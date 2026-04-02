

# WEEK 11 - OBJECT ORIENTED PROGRAMMING

## How OOP Applies Across Project Plan

Object-Oriented Programming is central to this project because every design pattern required to implement it is rooted in OOP concepts classes, objects, encapsulation, inheritance, and polymorphism.

Encapsulation shows up most clearly in the Singleton pattern. The TaskDatabase class hides the details of how data is stored and retrieved behind methods like save(), getAll(), and deleteById(). The rest of the STMS app never touches localStorage directly; it only interacts through the singleton instance. 

This keeps data logic contained in one place. 

For example:

\`class TaskDatabase {

  #tasks = \[\]; // private field

  constructor() {

    if (TaskDatabase.instance) return TaskDatabase.instance;

    this.#tasks = JSON.parse(localStorage.getItem('tasks')) || \[\];

    TaskDatabase.instance = this;

  }

  getAll() { return \[...this.#tasks\]; }

  save() { localStorage.setItem('tasks', JSON.stringify(this.#tasks)); }

}\`

Inheritance and Polymorphism come into play with the Factory pattern. Can define a base User class, then extend it for each role. Each subclass overrides a method like getPermissions() differently that's polymorphism. The factory doesn't care which subclass it's building; it just returns a User that responds to the same interface:

\`class User {

  constructor(name) { this.name = name; }

  getPermissions() { return \['read'\]; }

}

class Admin extends User {

  getPermissions() { return \['read', 'create', 'update', 'delete'\]; }

}

class Developer extends User {

  getPermissions() { return \['read', 'update'\]; }

}\`

The app calls user.getPermissions() regardless of the role it doesn't need to know whether it's dealing with an Admin or a Developer. That's the power of polymorphism.

Abstraction is demonstrated through the Observer pattern. We define a general notification system where any object can subscribe to task changes without knowing the internal details of how tasks work. The task just calls notify(), and each observer decides how to respond:

\`class Task {

  #observers = \[\];

  subscribe(observer) { this.#observers.push(observer); }

  setStatus(newStatus) {

    this.status = newStatus;

    this.#observers.forEach(obs => obs.update(this));

  }

}\`

Observers don't reach into the task's internals; they receive a clean update call. That's abstraction at work.

Composition over inheritance appears in the Decorator pattern. Instead of creating subclasses for every task variation (ReminderTask, TaggedTask, UrgentReminderTaggedTask...), we wrap a base task with decorators that add behavior:

\`class ReminderDecorator {

  constructor(task, reminderDate) {

    this.task = task;

    this.reminderDate = reminderDate;

  }

  getDetails() {

    return { ...this.task.getDetails(), reminder: this.reminderDate };

  }

}\`

This avoids deep inheritance chains and lets you mix and match features flexibly.

  

## Can HTML, CSS & JavaScript (my tech stack) Fully Support OOP?

The short answer is partially, but well enough for this project.

JavaScript supports OOP through ES6 classes, which give us constructors, inheritance with extends, method overriding, and private fields with the # syntax. For everything this project requires: Factory, Observer, Decorator, and Singleton. JavaScript's class system is fully capable.

Where it falls short compared to languages like Java or C# is in formal OOP features: there are no interfaces or abstract classes built into the language. You can't force a subclass to implement a specific method at compile time. There are no access modifiers like protected you get #private and public, nothing in between. And JavaScript's type system is dynamic, so you won't get compile-time errors if you pass the wrong object type somewhere.

The one genuine limitation worth noting is that HTML and CSS play no role in OOP; they handle structure and presentation. All OOP logic lives entirely in JavaScript. So my tech stack supports OOP through one of its three technologies, which is normal for a frontend project.