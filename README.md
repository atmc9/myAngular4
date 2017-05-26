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
    1. String Interpollation: {{ VariableName }} , {{ functionName(param1)  // that retuns a string }}, {{ condition? class1 : class2}} etc
    2. PropertyBinding: <button [disabled]="!allowButton"></button>. Dont mix the propertybinding and stringInterpollation [disabled]="{{!allowButton}}". This will break. 
    3. Event Binding: 

### Directives ###

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

