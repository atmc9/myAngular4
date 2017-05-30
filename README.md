# myAngular4App
Angular 4 Udemy tutorial project


## Project setup: ##
* We installed the nodejs and install the Angular cli using the command : `npm install -g @angular/cli`
* Creating a new app using: `ng new myAngular4App`
* Server the app by: `ng serve` - Typescript needs to be compiled to Javascript, starts a development server and runs the app at address http://localhost:4200 
* Updating the npm: `npm install -g npm`   
* Updating the angular-cli: `npm uninstall -g angular-cli @angular/cli;  npm cache clean; npm install -g @angular/cli`
* `ng-model` in angularJS is replaced by `[(ngModel)] = "property"`
* TypeScript: Superset to Javascript offers: Types, Classes, Interface
* How Angular App starts: The main.ts file knows which app module is in use AppModule and AppModule.ts bootstraps the components it has say AppComponent which has the HTML, css files to be used for this component. A few javascipt files are added at the bottom of our index file during ng serve.

### Components & Databinding: ###
* I can create a component using CLR `ng g c MyComponent` or can create a new MyComponent folder and add the TypeScript file with MyComponent.Component.ts name and MyComponent.Component.html files. Components are a way to seperate the UI modules(piece if independent HTMl,Frontend Business Logic, CS). 
* Databinding: Can be done using 4 ways
    1. String Interpollation: `{{ VariableName }}` , {{ functionName(param1)  // that retuns a string }}, {{ condition? class1 : class2}} etc
    2. PropertyBinding: `<button [disabled]="!allowButton"></button>` Dont mix the propertybinding and stringInterpollation [disabled]="{{!allowButton}}". This will break. 
    3. Event Binding: `<button (click)="functionName()"></button>`   // we can use any event name mouseenter, mouseleave, etc
       We can even use `(input)="onInputName($event)"`   and the `$event will pass the information about the event` what input is texted. you can access that data in you function as event.target.value whoch might need typecast (<HTMLInputElement>event.target).value. 
    4. Two-way Binding: `[(ngModel)]="myVariable"` this does the magic in 2-way :P. For this to work you need to import FormsModule from `@angular/forms` on your main app module.
    
### Directives ###
* Directives are instructions in the DOM. When we use component selector name on the DOM, we are kind of instructing the dom to render the template in our component. **Component are directives, but with a template.**  We typically add directive with attribute selector, can be configured as css class or element.    
* Example: `<p appTurnGreen> Receive a Green Background! </p>
    @Directive({    
        selector:'[appTurnGreen]'        
    })    
    export class TurnGreenDirective { .... }   `
* Structural directives like  `<p *ngIf="boolCondition"> The condition is true</p>` will change the DOM require * before directivename.     `<p *ngIf="boolCondition; else falseTemplate"> The condition is true</p>`
    `<ng-template #falseTemplate>The condition is false</ng-template>`
* Attribute directives: They dont add or remove elements. They only change the element they were placed on. `<p [ngStyle]="backgroundColor: getColor()"></p>`. `[ngClass]="{myClass: true}"`
* ngFor(Structural directive) `*ngFor="let item of itemslist; let i = index"` 

## New Project setup: 
* New Angular Course Project Creation: ng new ng4-Complete-Guide;  npm install --save bootstrap ; ng g c component --spec false // does not creates the test files; 
* ``Please see my fullstack developer reading material for Bootstrap navigation ``
* Create model where-ever make sense, use the shortcut of Typescipt for creating a model construtor(public name: string, pubic count: number){}
* Debugging help: When I put a break point on my main.bundle.js I opens the typescript file using source map or else I can open my webpack folder typesciprt files. **Useful debugging tool: Augury**
* How to achieve the inter component communication: Property and Event binding on our directives like in ngClass, ngStyle with this approach, also we can use it on our own components and bind them on custom properties and custom events. 
* **Custom Property Binding:** This can be done by making our component properties exposed by decorating with **@Input()** imported from '@Angular/core'. You can even alias by @Input('myAliasElement'). 
* **Custom Event Binding:** You can emmit events from your components by setting a property assigned with `eventCreated = new EventEmitter<datatype>` and finally emmit this in a function by saying `this.eventCreated.emit({object of datatype});`. Make sure you add the @Output before your property as you are emitting event outside of component. Youcan add alis of event as @Output('EventAlias')
* The Event and Property binding is very good to use in scenarios to communicate with parent or child components, but if the hop distance increases it is recomended to use the services for component communication. By default CSS applies only to our component. 
* **View Encapsulation in Angular:** The Html of an Component is Encapsulated using templateUrl and CSS using styleUrls. Very important note is CSS styles does not apply to all components it is acheived by angular by adding attributes of all its component elements(Kind of emulates shadow DOM). You can change 'encapsulation: ViewEncapsulation.Emulated(default)' // None(any css added to this component will be applied global, attributes are not added specific to your component), Native (Uses the Shadow DOM technology but only works with browser that support Shadow DOM )
* **Local references in templates and @ViewChild:** We can declare #LocallVariable as a refernce to an element and can pass to function as parameter or it can be also fetched using @ViewChild('LocallVariable') locallVariable : ElementRef; and can be used as this.locallVariable.nativeElement.value to get the value from DOM. Better to not set values on Dom, just use it to read values. 
* ng-content: You can set the markup between your custom component tags by using ng-content directive in your html template of component where your dynamic content needs to go.

* **Lifecycle of components:** 
    1. ngOnChanges - called after a bound input property changes
    2. ngOnInit - called once the component is initialized. It runs after the constructor. 
    3. ngDoCheck - called during every change detection run - called twice in development mode, as angular has extra change detection cycle. 
    4. ngAfterContentInit - called after content(ng-content) has been projected into view. If your component has ng-content dynamically passed between the component seletor tags, and if that content has a localVariable, you can access it by @ContentChild() and the element is only avialable after the ngAfterContentInit event. 
    5. ngAfterContentCheck - called everytime the projected content has been checked. 
    6. ngAfterViewInit - called after the componet's view (and child views) has been initialized. You can access the @ViewChild() elements data only after this event.
    7. ngAfterViewChecked - called every time the view(and child views) have been checked. 
    8. ngOnDestroy - called once the component is about to be destroyed
* Creating Directives: @Directive({selector: [appBasicHighlight]}) in its construtor we can access the Element that this directive is being used Ex: `constructor(private elementRef: ElementRef){} ngOnInit(){this.elementRef.nativeElement.style.backgroundColor = 'green'};`
* Better approach to access DOM in a Directive is using Renderer Ex: `constructor(private elementRef: ElementRef, private renderer: Renderer2){}  ngOnInit(){this.renderer.setStyle(this.elementRef.nativeElement, 'background-color','green'); }`. More about Render at : https://angular.io/docs/ts/latest/api/core/index/Renderer2-class.html. You can even listen to the events on the host by using `@HostListener('mouseenter') mouseover(){}`
* 

### Services & Dependency Injection ###

### Routing ###

### Observables ###

### Forms ###

### Pipes ###

### Http ###

### Authentication ###

### Optimizations & NgModules ###

### Deployment ###

### Animations & Testing ###

