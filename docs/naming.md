### Error handling:

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



