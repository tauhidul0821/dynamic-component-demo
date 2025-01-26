https://stackblitz.com/edit/stackblitz-starters-8qaphyv7?file=package.json

```ts
// main.ts

import { Component } from "@angular/core";
import { bootstrapApplication } from "@angular/platform-browser";
import {
  ViewChild,
  ViewContainerRef,
  ComponentFactoryResolver,
} from "@angular/core";
import { DynamicComponent } from "./app/dynamic/dynamic.component";
import { DynamicUsingFactoryResolverComponent } from "./app/dynamic-using-factory-resolver/dynamic-using-factory-resolver.component";

@Component({
  selector: "app-root",
  template: `
    <h1>Hello from {{ name }}!</h1>

    <button (click)="loadDynamicComponent()">
      Load Component Using ComponentFactoryResolver</button
    ><br />
    <ng-template #dynamicContainer></ng-template><br />

    <button (click)="loadDynamicComponent2()">Load Component 2</button>
    <ng-template #dynamicContainer2></ng-template>
  `,
})
export class App {
  name = "Angular";
  @ViewChild("dynamicContainer", { read: ViewContainerRef })
  container!: ViewContainerRef;
  @ViewChild("dynamicContainer2", { read: ViewContainerRef })
  container2!: ViewContainerRef;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  loadDynamicComponent(): void {
    const componentFactory =
      this.componentFactoryResolver.resolveComponentFactory(
        DynamicUsingFactoryResolverComponent
      );

    this.container.clear();
    this.container.createComponent(componentFactory);
  }

  loadDynamicComponent2(): void {
    this.container2.clear();
    this.container2.createComponent(DynamicComponent);
  }
}

bootstrapApplication(App);
```
