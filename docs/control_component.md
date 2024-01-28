## Control component (HOC)

A "Control Component" in refer to a component that is responsible for coordinating or controlling the behavior of other components. It could be a higher-level component that manages the state, data flow, and interaction between child components. We can also call it as "container component" or a "smart component" in Angular architecture.

<small style="color: red">Press down to see examples.</small>  



## Example of control component


```ts
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-control',
  template: `
    <app-child1 [data]="sharedData" (update)="handleUpdate($event)"></app-child1>
    <app-child2 [data]="sharedData"></app-child2>
  `,
})
export class ControlComponent implements OnInit {
  sharedData: any;

  constructor(private dataService: DataService) {}

  ngOnInit(): void {
    this.loadData();
  }

  loadData(): void {
    this.dataService.getData().subscribe((data) => {
      this.sharedData = data;
    });
  }

  handleUpdate(updatedData: any): void {
    // Handle data update from child1
    this.dataService.updateData(updatedData);
  }
}
```