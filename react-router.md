# React Router: Overview



Hey there! As of now, we are able to spin up a fresh React application with Vite, get rid of some files we won’t use and then set up some things we will, like TailwindCSS. But as our application grows, having all the content in the same visual space doesn’t feel ideal. Imagine a eCommerce site where the landing page is an overview of all the products, but then you can navigate to `/cart` to check your shopping cart, or to `/myAccount` to check your account details. This navigation-content relationship is what we are about to learn now.

Specifically, we are going to learn how to do this in the conext of a **Single-Page Application** with **React** and an amazing library called [**React Router**](https://reactrouter.com/start/declarative/installation)

### First things first: What is Routing in an Application?

Routing is the mechanism by which we navigate through different parts of a web application. It helps in defining how users move between different views or pages.

In traditional multi-page applications (MPAs), each click on a link leads to a new request to the server, fetching a new HTML page.

![](https://learn.wbscodingschool.com/wp-content/uploads/2024/06/Screenshot-2024-06-24-at-10.55.11.webp)

However, in modern single-page applications (SPAs), routing is handled on the client-side. This means that instead of loading a new page from the server, the application dynamically changes its state and updates the view to simulate navigation. All this is done and orchestrated with JavaScript via asynchronous requests (AJAX, Asynchronous JavaScript and XML).

![](https://learn.wbscodingschool.com/wp-content/uploads/2024/06/Screenshot-2024-06-24-at-10.58.27.webp)

### Single-Page Application (SPA) and Routing

In a single-page application, all necessary code (HTML, CSS, JavaScript) is loaded once, and subsequent interactions only update parts of the page. This makes SPAs feel faster and more responsive. When routing in an SPA, the URL changes as the user navigates, but the page does not fully reload. This is achieved through client-side routing.

Even with routing, an SPA remains an SPA because:

- Only one HTML file is loaded initially.
- Subsequent navigations do not trigger full page reloads.
- The content dynamically changes based on the route.

### Browser Router and the History API

[**React Router**](https://reactrouter.com/start/declarative/installation) provides a declarative way to handle routing in a React application. It’s a React, component-based library that keeps track of changes in the navigation by plugging our application with the [**History API**](https://developer.mozilla.org/en-US/docs/Web/API/History_API) by default, it uses state to keep an internal reference of where the user has navigated to and, based on that, display the appropriate content. Just a very smart and optimised conditonal rendering library that listens for changes to the navigation.

**Key Points About React Route:**

- **Declarative Routing**: Define routes in a declarative manner, making the code more readable and maintainable.
- **URL Management**: Change the URL and manage the browser history without causing a full page refresh.
- **Dynamic Route Matching**: Match URLs to components dynamically, allowing for a flexible and dynamic navigation system.

### Setting Up React Router

### Installation

[**React Router**](https://reactrouter.com/start/declarative/installation) is available via de `npm` registry so it can be installed accordingly

```bash
npm i react-router
```

### Basic Setup

React Router offers different types of routers for different scenarios. From a basic declarative approach using components to using it as a framework! We are going to start simple with the `BrowserRouter` which implements the History API.

[https://playground.wbscod.in/react/react-router/1](https://playground.wbscod.in/react/react-router/1)

This example demonstrates how to build a simple single-page application (SPA) using **React Router in Declarative Mode**. Declarative routing is one of the three primary ways to use React Router (alongside Data Mode and Framework Mode), and it's by far the most accessible and beginner-friendly. It allows you to define your application's navigation structure using components, making routing clear and maintainable.

In this example, we set up three pages—**Home**, **About**, and **Contact**—wrapped in a shared layout that includes a navigation bar.

**1. Importing the Essentials**

The application uses key features from `react-router`, including:

- `BrowserRouter`: Sets up client-side routing.
- `Routes` and `Route`: Define the route structure.
- `Link`: Enables navigation without full page reloads.
- `Outlet`: A placeholder for rendering matched nested routes.

These building blocks form the foundation of declarative routing in React.

**2. Setting a Base Path**

The `basename` is set to `/wbs-live-examples-target`. This is only needed because our preview app runs within a GitHub Pages environment, which serves the app under a subdirectory. In most production or development scenarios, you can omit this configuration.

**3. Navigation with the Navbar Component**

The `Navbar` component displays a horizontal navigation bar with links to the three main pages. It uses `Link` components, which allow navigation between routes without reloading the page—crucial for maintaining SPA behavior.

**4. Layout with MainLayout**

`MainLayout` wraps the content for all main routes. It includes the `Navbar` and an `Outlet`, which dynamically renders the component that matches the current nested route. This approach keeps layout structure consistent across all pages.

**5. Defining Pages as Route Components**

The `Home`, `About`, and `Contact` components represent individual pages. Each one returns a simple piece of content, and they are mapped to their respective routes under the `/` path.

**6. Declarative Routing Configuration**

Routing is defined as follows:

- The root path (`"/"`) is handled by `MainLayout`, establishing a layout route.
- Nested within it are three child routes:
    - The **index route** renders `Home` when the path is exactly `/`.
    - The `about` and `contact` routes render their corresponding components.
