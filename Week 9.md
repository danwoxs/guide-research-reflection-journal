# WEEK 9 - DESIGN PATTERNS

## RESEARCH ON DESIGN PATTERNS

Design patterns are standardized, reusable solutions to recurring problems in software architecture, serving as a blueprint for developers. Among creational patterns, the Singleton pattern ensures that a class has only one instance while providing a global point of access to it (Gamma et al., 1994). In real-world applications, this is vital for centralized resource management; for example, a system's logging service or a database connection pool uses a Singleton to prevent data corruption and ensure all parts of an application record information to the exact same file. Another essential creational pattern is the \*\*Factory Method\*\*, which defines an interface for creating an object but allows subclasses to alter the specific type of objects being created (Freeman et al., 2004). A concrete example is a cross-platform mobile application where a core \`DocumentCreator\` delegates the instantiation process, seamlessly generating either a PDF document object or a Word document object depending on the user's selected export settings.

Transitioning to behavioral patterns, the Observer pattern defines a one-to-many dependency between objects so that when a core object changes state, all its dependents are automatically notified and updated (Gamma et al., 1994). This is the backbone of event-driven software and modern user interfaces; a practical example is a stock market application where a central server updates a stock's price, instantly triggering automatic visual updates across multiple linked components like a user's portfolio dashboard, a live ticker widget, and an SMS alert system. Similarly, the Strategy pattern focuses on behavior by encapsulating a family of algorithms and making them completely interchangeable at runtime without altering the client code that uses them (Freemant al., 2004). A concrete application of this is a navigation app; the core interface remains exactly the same, but the app dynamically swaps out complex routing algorithms (strategies) based on whether the user clicks the icon for driving, walking, or public transit directions.

Ultimately, the integration of these four design patterns - Singleton, Factory Method, Observer, and Strategy demonstrates how developers can architect robust, flexible software systems that gracefully anticipate future growth. By deliberately isolating the creation of objects and the delegation of complex behaviors, these patterns reduce tight coupling and prevent the rigid, intertwined code that often plagues large-scale projects (Shalloway & Trott, 2001). Beyond solving immediate technical hurdles, utilizing these established templates provides software engineering teams with a shared, highly efficient vocabulary, ensuring that architectural decisions are easily communicated, maintained, and scaled across different teams and generations of developers.

  
## HOW TO CONTRIBUTE TO OPEN SOURCE

Contributing to an open source project involves a collaborative process for beginners. It is worth noting that valuable contributions extend far beyond writing code. It encompasses everything from user interface design and documentation to event organization and issue triage. It is important to first "read the room" by familiarizing yourself with a project's anatomy such as its README, Contributing guidelines, and Code of Conduct before communicating clearly, asking context-rich questions, and opening a draft pull request to invite early feedback.

As a beginner front-end developer with a lot of interest in User Experience (UX), I can start by contributing to:

-   First Contributions: a hands-on repository specifically designed to teach the pull-request workflow
    
-   freeCodeCamp: a massive open-source educational platform that frequently needs UI improvements and CSS fixes
    
-   OpenSauced: a tool for tracking open-source engagement that actively welcomes React and front-end component updates
    
-   The A11y Project: a community-driven initiative dedicated to web accessibility, making it an ideal space to apply human-computer interaction and modern interface design principles
    

## FIND POTENTIAL PROJECTS TO CONTRIBUTE TO

Google Lighthouse is a vital open-source tool used by developers to audit and improve web page performance, accessibility, and SEO. I see a perfect opportunity to contribute to this industry-standard tool by addressing Issue #15877. This issue concerns the lack of visual feedback, specifically the inability for a user to click on timeline images to open the full-size images.

My contribution will focus on enhancing this visual feedback by implementing a hover interaction to display the full image. This task is an excellent entry point for applying my front-end development skills in a production codebase, offering valuable practice in precise styling, interactive design, and contributing to the maintenance of a widely-used project.


## BIBLIOGRAPHY

1.  Freeman, E., Robson, E., Bates, B., & Sierra, K. (2004). \*Head first design patterns\*. O'Reilly Media.
    
2.  Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). \*Design patterns: Elements of reusable object-oriented software\*. Addison-Wesley.
    
3.  Shalloway, A., & Trott, J. R. (2001). \*Design patterns explained: A new perspective on object-oriented design\*. Addison-Wesley Professional.