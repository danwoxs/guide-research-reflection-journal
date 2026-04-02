
# WEEK 10 - MV\* PATTERNS

## SUMMARY

MV\* patterns are architectural blueprints designed to separate the visual interface of an application from its underlying data and business logic, making code significantly easier to read, test, and maintain. The foundational pattern in this family is Model-View-Controller (MVC), where the Model manages the raw data, the View handles the user interface, and the Controller acts as the brain-taking user input, updating the Model, and telling the View to refresh. 

A stricter variation of this is Model-View-Presenter (MVP), which completely cuts off direct communication between the View and the Model. In MVP, the Presenter handles all the UI logic and updates a passive View through a strict interface, a design that makes writing automated tests for the logic much easier because the visual elements are entirely isolated.

Building on these ideas to handle modern, highly interactive interfaces, the Model-View-ViewModel (MVVM) pattern introduces a powerful concept called "data binding." In MVVM, the ViewModel acts as the bridge, but instead of the developer writing manual code to update the screen, the View automatically observes and reacts to data changes in the ViewModel. This creates a seamless, automated synchronization; when underlying data updates, the UI instantly reflects it, and when a user types in a form, the data updates automatically. Because it removes the need for repetitive UI update code, MVVM has become the standard architectural choice for modern reactive frameworks like Angular, Vue, and contemporary mobile app development.
