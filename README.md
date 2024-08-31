# Angular Components Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Component Metadata](#component-metadata)
4. [Component Lifecycle Hooks](#component-lifecycle-hooks)
5. [Component Communication](#component-communication)
6. [Input and Output Decorators](#input-and-output-decorators)
7. [Component Styles](#component-styles)
8. [View Encapsulation](#view-encapsulation)
9. [Dynamic Components](#dynamic-components)
10. [Component Inheritance](#component-inheritance)
11. [Conclusion](#conclusion)

## Introduction

An **Angular Component** is a core building block of Angular applications, encapsulating a portion of the user interface. Each component manages its own view and logic, making it reusable and modular. Components are made up of three key elements:
1. **TypeScript Class**: Manages component logic and data.
2. **HTML Template**: Defines the structure and layout of the component's view.
3. **CSS/SCSS Styles**: Specifies the appearance of the component.

---

## Component Structure

An Angular component typically consists of the following files:

1. **TypeScript File (`.ts`)**:
   Contains the class, logic, and methods for the component.

2. **HTML Template (`.html`)**:
   Defines the HTML structure and bindings for the component's view.

3. **CSS/SCSS File (`.css` or `.scss`)**:
   Provides styles specific to the component.

4. **Spec File (`.spec.ts`)** (Optional):
   Contains unit tests for the component.

### Example Component:

1. **Component Class (`hello-world.component.ts`)**:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello-world',      // Custom HTML tag for this component
  templateUrl: './hello-world.component.html',  // Path to the HTML template
  styleUrls: ['./hello-world.component.css']    // Path to the CSS/SCSS styles
})
export class HelloWorldComponent {
  message: string = 'Hello, World!';   // Property used in the template

  // Method to update the message property
  updateMessage(newMessage: string) {
    this.message = newMessage;
  }
}
Component Template (hello-world.component.html):
html
Copy code
<div>
  <h1>{{ message }}</h1>  <!-- Data binding for the message property -->
  <button (click)="updateMessage('Hi, Angular!')">Change Message</button>
</div>
Component Styles (hello-world.component.css):
css
Copy code
h1 {
  color: blue;
}

button {
  background-color: #007bff;
  color: white;
  padding: 10px;
}
Component Metadata
The @Component decorator provides metadata that Angular uses to configure and instantiate the component. This metadata includes:

selector: Defines the custom HTML tag to use for the component.
templateUrl: Points to the HTML file for the component's view.
styleUrls: Specifies paths to CSS/SCSS files for component-specific styles.
providers: Lists services available to this component.
animations: Specifies animations applied to the component.
Example:
typescript
Copy code
@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  styleUrls: ['./example.component.css'],
  providers: [ExampleService],
  animations: [exampleAnimation]
})
Component Lifecycle Hooks
Angular components have a lifecycle with several phases. Lifecycle hooks are methods that allow you to execute code at different stages of a component's life.

Common Lifecycle Hooks:
ngOnInit: Called once the component is initialized.
ngOnChanges: Invoked when input properties change.
ngOnDestroy: Called before the component is destroyed.
Example:
typescript
Copy code
export class LifecycleComponent implements OnInit, OnDestroy {
  
  ngOnInit() {
    console.log('Component initialized');
  }

  ngOnDestroy() {
    console.log('Component destroyed');
  }
}
Component Communication
Components often need to communicate with each other. This can be achieved using @Input and @Output decorators.

1. Parent to Child Communication:
Use the @Input decorator to pass data from a parent component to a child component.

2. Child to Parent Communication:
Use the @Output decorator with an EventEmitter to send data from a child component to a parent component.

Input and Output Decorators
@Input:
The @Input decorator allows a parent component to bind properties to a child component.

typescript
Copy code
export class ChildComponent {
  @Input() childMessage: string;  // Message passed from the parent
}
@Output:
The @Output decorator allows a child component to emit events to the parent component.

typescript
Copy code
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Hello from Child!');
  }
}
Component Styles
Each Angular component can have its own styles, scoped specifically to the component. This prevents styles from leaking out or affecting other components.

Example:
css
Copy code
h1 {
  color: red;
}
Inline Styles:
Styles can also be defined directly in the @Component decorator using the styles array.

typescript
Copy code
@Component({
  selector: 'app-inline-style',
  template: `<h1>Inline Styled Component</h1>`,
  styles: [`h1 { color: green; }`]
})
View Encapsulation
Angular provides three encapsulation modes to control how styles are applied to components:

Emulated: Default mode. Styles are scoped to the component.
None: No encapsulation. Styles are applied globally.
Shadow DOM: Uses Shadow DOM for encapsulation.
Example:
typescript
Copy code
@Component({
  selector: 'app-encapsulation',
  template: `<h1>Encapsulation Example</h1>`,
  encapsulation: ViewEncapsulation.None   // No encapsulation
})
Dynamic Components
Dynamic components can be created and inserted into the view at runtime using Angular’s ComponentFactoryResolver.

Example:
typescript
Copy code
@Component({
  selector: 'app-dynamic-component',
  template: `<ng-container #container></ng-container>`
})
export class DynamicComponent implements AfterViewInit {
  @ViewChild('container', { read: ViewContainerRef }) container;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  ngAfterViewInit() {
    const componentFactory = this.componentFactoryResolver.resolveComponentFactory(SomeOtherComponent);
    this.container.createComponent(componentFactory);
  }
}
Component Inheritance
Component inheritance allows you to reuse code by extending a base component class.

Example:
typescript
Copy code
export class BaseComponent {
  message: string = 'Hello from Base Component';
}

@Component({
  selector: 'app-child-component',
  template: `<p>{{ message }}</p>`
})
export class ChildComponent extends BaseComponent { }
Conclusion
Angular components are essential for building modular, reusable, and maintainable applications. Understanding their structure, metadata, lifecycle hooks, communication patterns, and styles is crucial for effective Angular development.
