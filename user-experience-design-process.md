# User Experience Design Process

### User Experience becomes a Key Success Factor

In the past, we focused mainly on building products that fulfilled the functional requirements of the user. User experience was often considered late in the development process. But today the customer demands more than just a working product. Providing the right features is still the prerequisite for a good product, but to turn it into something extraordinary you need to provide a good user experience!

Providing a rich user experience is not a thing of fortune. It needs to be planed, designed and integrated into the development of a product. Designing a rich user experience is not only about make up your user interface by some graphics and gradients - its a much broader concept. Its about creating an emotional connection between the user and your software. It makes the user feel good and so he likes to continue using the software.

New Tools for Designers

Microsoft recognized, give development teams the power to create rich user experiences it needs a lot more graphical tool support than VisualStudio can provide today. So they decided to create a new tool suite - made for designers.


This tool suite is called Microsoft Expression. It consists of the four products:

Expression Blend is built to create user interfaces in WPF and Silverlight. It builds the bridge between designer and developers. It can open VisualStudio solutions
Expression Design is a leightweight version of Adobe Illustrator to create and edit vector graphics.
Expression Media is built to encode, cut and enrich video files and optimize them for silverlight streaming
Expression Web is Microsoft next generation of HTML and Javascript editor. Its the replacement for Frontpage.
Together they are a powerful package. The following illustration shows a sample workflow of integrating a vector image that is created by a graphics designer in Adobe Illustrator into a WPF project that is part of a VisualStudio solution.


Development Workflow of a WPF Project

Developing a WPF application with a rich user experience requires a lot more skills than just a requirements analyst that defines a list of use cases and developer that implements the software. You have to find out what the user really needs. This can be done by following a user centered approach.


1. Elicit Requirements

Like in any kind of software projects its important to know and focus the target of your development. You should talk to stakeholders and users to find out the real needs. These needs should be refined to features and expressed in use cases (abstract) or user scenarios (illustrative). Priorize the tasks by risk and importance and work iteratively. This work is done by the role of the requirements engineer.

2. Create and Validate UI Prototype

Creating a user interface prototype is an important step to share ideas between users and engineers to create a common understanding of the interaction design. This task is typically done by an interaction designer. It's helpful to only sketch the user interface in a rough way to prevent early discussions about design details. There are multiple techniques and tools to do this. Some of them are:

Paper prototype
Use paper and pencil to draw rough sketches of your user interface. No tools and infrastructure is needed. Everyone can just scribble thier ideas on the paper.
Wireframes
Wireframes are often used to sketch the layout of a page. It's called wireframes because you just draw the outlines of controls and images. This can be done with tools like PowerPoint or Visio
Expression Blend 3 - Sketch Flow Sketch flow is a new cool feature to create interactive prototypes directly in WPF. You can use the integrated "wiggly style" to make it look sketchy. The prototype can be run in a standalone player that has an integrated feedback mechanism.
Interactive Prototype The most expensive and real approach is to create an (reusable) interactive prototype that works as the real application but with dummy data.
It is strongly recommended to test your UI prototype on real users. This helps you to find out and address design problems early in the development process. The following techniques are very popular to evaluate UI prototypes:
Walktrough
A walktrough is usually done early in a project with wireframes or paper prototypes. The user gets a task to solve and he controlls the prototype by touching on the paper. The test leader than presents a new paper showing the state after the interaction.
Usability Lab
To do a usability lab, you need a computer with a screen capture software and a camera. The proband gets an task to do and the requirements and interaction engineer watch him doing this. They should not talk to him to find out where he gets stuck and why.
3. Implement Business Logic and Raw User Interface

4. Integrate Graphical Design

5. Test software

Roles

Buliding a modern user interface with a rich user experience requires additional skills from your development team. These skills are described as roles that can be distributed among peoples in your development team.

Developer
The developer is responsible to implement the functionality of the application. He creates the data model, implements the business logic and wires all up to a simple view.
Graphical Designer
The graphical designer is responsible to create a graphical concept and build graphical assets like icons,logos, 3D models or color schemes. If the graphical designer is familiar with Microsoft Expression tools he directly creates styles and control templates.
Interaction Designer
The interaction designer is responsible for the content and the flow of a user interface. He creates wireframes or UI sketches to share its ideas with the team or customer. He should validate his work by doing walktroughs or storyboards.
Integrator
The integrator is the artist between the designer and the developer world. He takes the assets of the graphical designer and integrates them into the raw user interface of the developer. This role needs a rare set of skills and so it's often hard to find the right person for it.
More Infos

The New Iteration - Microsoft Paper about the Designer/Developer collaboration 
