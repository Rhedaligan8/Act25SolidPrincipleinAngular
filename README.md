ACTIVITY 25: SOLID PRINCIPLES in Angular | Aligan, Rhed N.

What is SOLID Principle?
The SOLID principles are a set of five guidelines that help software developers write cleaner, more flexible, and maintainable code. They are intended to make code easier to understand, easier to change, and less likely to produce bugs. Following these principles helps create software that is modular and adaptable to future changes.

In addition, there’s a different strategy or methods based on what will be the output of the product or program. This will help to be scalable and maintainable for the rapid changes of development technology.

In Angular, applying a SOLID principle also as an acronym help the developers of angular create more flexible, scalable, and maintainable program. There’s a different principle that can be use depends on what wanted to achieve for the output.

S - Single Responsibility Principle (SRP):

As the named mentioned, there’s only a one role or job will be used per component to make the program works smoothly in a specific area. It prevents to damage other who are not totally included in the type of error or bag. In angular application, this will be effective to not make a damage other that making it easy to change one without affecting the other.
Practical Applications

To make easier to understand, let’s use an illustration in a real-life situation. For instances, in our business named “JoRhe Bliss Shop” we have a delivery rider to serve, and an employee to package products. Now when the products damaged due to the arrival cause of the rain, the only need you to confront is the delivery rider not the employee to package products.
In angular, within the system you need only to investigate the components or modules who are handle with the specific task such as deliver process just in case of trouble and bugs without affecting others or not totally involved of that circumtances. This will help reduce the chance of one service or action affecting’s others.

Code Snippets


Copy

Copy
// Good: The component focuses on presentation, and the service handles the data logic.
@Component({
  selector: 'app-user-profile',
  templateUrl: './user-profile.component.html',
})
export class UserProfileComponent {
  userData: any;

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.userService.getUserData().subscribe(data => this.userData = data);
  }
}

@Injectable({
  providedIn: 'root',
})
export class UserService {
  constructor(private http: HttpClient) {}

  getUserData() {
    return this.http.get('/api/user');
  }
}
With this code snippets show two different methods include of UserProfileComponent for the components and the UserService for the service, The components do task is to present or the display data in the service, while service is the fetching and retrieving data from the system input.

The UserProfileComponent doesn’t have power to fetch and retrieve the data, only display and present. Otherwise, UserService can do.

Between two of them, if you need modify or update the API endpoint like /api/v2/user for update the version, only the UserService can modify, not the UserProfileComponent, Vise versa, if you need change the display or what need to present, only the UserProfileComponent can modify and the UserService wouldn’t need to change.

Open/Closed Principle (OCP):

In OCP, use to make adapting and scalable system without affecting others already exists or working. This will help prevent damage other functionalities and service while adding a new features and modules in the system. Instead of overwriting or rewriting the whole system and services, instead add on the process so it can easily growth without disrupting other components working. The component should be open for adaption and extension and close for modifications.
Practical Applications

In example of application in real-life, let’s use a restaurant that have a different dish. Overtime, there’s a new dish added on the menu, using OCP the other menu already exist is not disrupt or move otherwise, it can be adaptive or add more a new dish without affecting other’s functionality.
In angular, it helps allow new features or changes without modifying existing code. This is especially useful when adding new functionality to a component or service. Angular makes this possible through inheritance, decorators, and modular architecture.

Code Snippets


Copy

Copy
// Good: Open for extension, closed for modification using a strategy pattern.
@Injectable({
  providedIn: 'root',
})
export abstract class DiscountStrategy {
  abstract getDiscount(): number;
}

@Injectable({
  providedIn: 'root',
})
export class PremiumDiscountStrategy extends DiscountStrategy {
  getDiscount() {
    return 20;
  }
}

@Injectable({
  providedIn: 'root',
})
export class RegularDiscountStrategy extends DiscountStrategy {
  getDiscount() {
    return 10;
  }
}

@Injectable({
  providedIn: 'root',
})
export class DiscountService {
  constructor(private discountStrategy: DiscountStrategy) {}

  getDiscount() {
    return this.discountStrategy.getDiscount();
  }
}
In code snippets above shows, a strategy pattern how the OCP works. as you can see abstract class that defines the structure (interface) for the discount strategy. It declares an abstract method getdiscount(), which every subclass must implement.

It's open for extension because we can add new discount strategies by creating new subclasses (e.g., SeasonalDiscountStrategy), but closed for modification because the core logic (in DiscountService) doesn't need to change to add new strategies.

We can add more class for example above like DiscountSenior or DiscountStudent effect of 20% discount extends on the DiscountStrategy without modifying existing code.

Liskov Substitution Principle (LSP):

In Liskow Substitution principle, works with which emphasizes that objects of a derived class should be able to replace objects of the base class without altering the correctness of the program. In other words, if a class is a subclass of another, it should be able to be used in place of the parent class without causing issues, such as unexpected behavior or errors. In the word substitution is can be an option or choice from the original class or component without breaking the program or system.
Practical Applications

In the practical applications, for example you have an application that have a payment option, you can add class within the component or components to make a substitute choice to process payment via credit card, electronic wallet, or cash. so, the quality of service such as payment method can operate simultaneously without affecting the original or default option.
In Angular, this is helpful for creating reusable components and services that follow predictable behaviors. If you have payment based such as payment method, you can add a class extend on the name of another class such as the class name of Credit/Debit Card, E-Wallet, and Cash without crashing the app while altering or changing option.

Code Snippets


Copy

Copy
// Base class
@Injectable({
  providedIn: 'root',
})
export class BaseLogger {
  log(message: string) {
    console.log(`Base log: ${message}`);
  }
}

// Subclass that extends the base class
@Injectable({
  providedIn: 'root',
})
export class CustomLogger extends BaseLogger {
  log(message: string) {
    super.log(`Custom log: ${message}`);
  }
}

// Using the logger service
@Injectable({
  providedIn: 'root',
})
export class SomeService {
  constructor(private logger: BaseLogger) {}

  doSomething() {
    this.logger.log('Suspicious Something');
  }
}
For example, in the code snippets above shows a BaseLogger who present all data, the CustomLogger class which extends on the BaseLogger. This class extends the BaseLogger class, meaning it inherits all its properties and methods.

The log method is overridden here to modify the behavior. Instead of just logging a message with the Base log: prefix, it calls super.log(), which invokes the logmethod of the base class(BaseLogger) but with a modified message prefixed with Custom log. SomeService, depends on a logger service. It is injected with the BaseLogger(or its subclass, if you choose to configure it differently).

So, in the SomeService can be able to retrieve data and if the Log is suspicious, it will be not display otherwise it shows suspicious Something, while the two class such as Base log and CustomLogger can be able to present and display the data into the strings any of that class without interrupting the quality service can provide.

Interface Segregation Principle (ISP):

In ISP, it find only what needed in the company or system, they not acquired to train or or simulate of what necessarily needed in the development. Clients should not be forced to depend on interfaces they don’t use. By focusing only on essential skills per role, you make training and day-to-day work simpler and more efficient.
In angular, keep your interfaces in Angular lean and focused on specific tasks, rather than creating large, all-encompassing interfaces. This results in cleaner code that’s easier to test and maintain. In simpler terms, it suggests breaking down large, general interfaces into smaller, more specific ones so that consumers only interact with the methods they actually need.

Practical Applications

In real-world use cases, for example in the programming or developers job seeker, the company has only need a java and php programmer, they only acquired and hire who are knowledgeable in a java and php for the java and php based project. This will help the project easily develop and deploy efficiently because they not hire other of not looking for since there’s a criterion.
In angular, this principle is applied through dependency injection, which allows high-level modules (like components) to depend on abstractions (interfaces or base classes) rather than on specific, low-level implementations. So, instead like in a service interface all methods like CRUD, you can focus on what need like only fetch and updater, but in a corporate world interview the more your knowledge is a great advantage even this is not the big deal for them since there’s requirements.

Code Snippets


Copy

Copy
// Good: Split responsibilities into smaller, focused services.
@Injectable({
  providedIn: 'root',
})
export class UserService {
  getUser() {
    // fetch user
  }

  updateUser() {
    // update user
  }
}

@Injectable({
  providedIn: 'root',
})
export class PermissionService {
  getUserPermissions() {
    // fetch permissions
  }
}
In this snippet, each service now has a clear, focused responsibility, making it easier to test and maintain. so with the class PermissionService to get the user permission data, need in the end of user allow or such as permit to get their data, so the data will be fetched and update and display on the class of component or class UserService. the PermissionService is handling to handling permissions.

Dependency Inversion Principle (DIP):

In ISP, shows generally how flexible our class and components to migrate when our system is dependent on the model or framework have. With this principle the workflow of the system still working without impact the workflow of the development. It can be adaptable for changes in equipment or technology have nowadays.
In angular, this principle is applied through dependency injection, which allows high-level modules (like components) to depend on abstractions (interfaces or base classes) rather than on specific, low-level implementations. With the same syntax and components, the code or program is compatible to migrate with a smaller modification in in service. It dependent on the Base class not in the other class under the base class so it can easily migrate and adapt.

Practical Applications

Your restaurant runs on universal systems, not on specific brands or models. For example, you use a general POS (Point of Sale) system that can be swapped out or updated if needed, without impacting your whole restaurant workflow. You’re not attach to a specific brand for cooking equipment either, so replacing a piece doesn’t affect your entire kitchen.

Code Snippets


Copy

Copy
// Good: Depend on abstractions instead of concrete implementations.
@Injectable({
  providedIn: 'root',
})
export class ProductService {
  constructor(private apiService: ApiService) {}

  getProducts() {
    return this.apiService.get('/products');
  }
}

@Injectable({
  providedIn: 'root',
})
export class ApiService {
  constructor(private http: HttpClient) {}

  get(endpoint: string) {
    return this.http.get(`/api${endpoint}`);
  }
}
In above snippets, you can easily replace the ApiService with another implementation, such as a mock API during testing, without modifying ProductService. It shows that high-level modules should not depend on low-level modules, but both should depend on abstractions. For that code The ProductService depends on the ApiService abstraction, not on a specific implementation of HTTP handling. ApiService is responsible for making HTTP requests but is designed in a way that it can be easily replaced or modified without affecting ProductService.

By using dependency injection (private apiService: ApiService), the ProductService is decoupled from the actual implementation details of how data is fetched, promoting flexibility and easier testing.

Conclusion
APPLYING SOLID PRINCIPLE especially in angular will help the developers to develop at the same time maintainable, scalable overtime while it can ably migrate with the same abstraction based on what principle will used. Not only the good writing at code but to anticipate the long-term use of the program will be. It can be able to prevent and avoid a spaghetti and complicated codebase since the goal of using of Principle is make our code readable and flexible over time.

Relevant Links/ Source of Article

The SOLID Principles in Angular: A Guide to Cleaner, Scalable Code | by Rengith Manickam(Ranjith) | Oct, 2024 |

https://angularindepth.com/posts/1414/angular-and-solid-principles
