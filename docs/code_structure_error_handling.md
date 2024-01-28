## Error handling

Failing to implement proper error handling can result in `unhandled exceptions` and make it challenging to identify and resolve issues.

<small style="color: red">Press down to see examples.</small>



### Good error handling:

To handle, observer error, `catchError` operator of rxjs is useful to catch the error. Here we can do 2 things:

- Throw the error directly in case we want to prevent next syntax to be executed.
- Make the error pass throw to be handled in different place. In this case, we need to return the error wrapped in `of` operator of rxjs

```ts [1-30|19-27]
private async httpCall<ArgsType, ResponseType>(
    args: ArgsType,
    resourcePath: string
  ): Promise<ResponseType> {
    return firstValueFrom(
      this.httpService
        .post<ResponseType>(
          `${this.contentServiceUrl}/api/${resourcePath}`,
          args,
          {
            headers: {
              'x-api-key': this.contentServiceApiKey,
              'content-type': 'application/json',
            },
          }
        )
        .pipe(
          map((res) => res.data),
          catchError((error: AxiosError) => {
            const responseBody = get(error, 'response.data');

            throw new InternalServerErrorException(
              `Error: ContentClientError! ${error.message} - ${JSON.stringify(
                responseBody
              )}`
            );
          })
        )
    );
  }
```



### Angular error handling

Usually Interceptor is suitable for all HTTP calls. However, it might cause some limitation controlling the errors. For that reason, we may consider individual service for error handling:


```ts
import { Injectable } from '@angular/core';
import { HttpErrorResponse } from '@angular/common/http';
import { throwError } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class ErrorHandlerService {
  constructor() {}

  handleHttpError(error: HttpErrorResponse): void {
    let errorMessage = 'An error occurred.';

    if (error.error instanceof ErrorEvent) {
      // Client-side error
      errorMessage = `Client Error: ${error.error.message}`;
    } else {
      // Server-side error
      errorMessage = `Server Error: ${error.message}`;
    }

    // You can log the error or send it to a logging service
    console.error(errorMessage);

    // You can also choose to rethrow the error or handle it differently based on your requirements
    // For demonstration purposes, we'll rethrow the error
    throw error;
  }

  handleNonHttpError(error: any): void {
    // Handle non-HTTP errors here (e.g., errors not coming from an HTTP request)
    console.error('Non-HTTP Error:', error);

    // You can choose to handle non-HTTP errors differently based on your requirements
    // For demonstration purposes, we'll rethrow the error
    throw error;
  }
}
```



### Service usage:

Can be used like the following:

```ts [17-18]
import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { ErrorHandlerService } from './error-handler.service';

@Component({
  selector: 'app-some',
  template: '<button (click)="makeRequest()">Make Request</button>',
})
export class SomeComponent {
  constructor(private http: HttpClient, private errorHandlerService: ErrorHandlerService) {}

  makeRequest(): void {
    this.http.get('https://example.com/api/data').subscribe(
      catchError((e: Error) => {

        // Upon condition, we can call either handleHttpError | handleNonHttpError
        this.errorHandlerService.handleHttpError(error);
        this.errorHandlerService.handleNonHttpError(error);
      })
    );
  }
}
```