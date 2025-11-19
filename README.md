Assignment 7

1. What is a widget tree in Flutter and how do parent-child relationships work between widgets?

In Flutter, every visual element is a widget, and these widgets are organized in a hierarchical data structure called the widget tree. The widget tree starts from the root and grows downward as widgets contain other widgets—this forms the parent-child relationship between them. A parent widget defines layout rules, styling, and constraints for its children, while children represent specific UI elements or behavior (such as text, buttons, or containers). Data typically flows downward from the parent to the child through constructor parameters or inherited widgets, while actions like button presses flow upward through callback functions or state management techniques. This architecture encourages a declarative and composable design, where complex UIs are built from smaller, reusable widget units.

2. List all the widgets you used in this project and explain their functions.

This project uses a range of built-in Flutter widgets to construct a functional and interactive UI while also incorporating custom widgets for modularity.

- MaterialApp: Sets up the application with Material Design elements, themes, and navigation.

- Scaffold: Serves as the basic page structure by providing areas for the app bar, body, floating buttons, drawer, and more.

- AppBar: Displays the app's title at the top of the screen within the Scaffold.

- Text: Renders static strings like the title or descriptions.

- Column & Row: Layout widgets that align children vertically (Column) or horizontally (Row).

- GridView.count: Displays interactive cards in a grid layout with a fixed number of columns (three in this case).

- Container: A versatile widget for styling, alignment, padding, and layout control.

- Card: Used to show information blocks with elevation and rounded corners.

- Icon: Displays graphical icons within the UI, such as grid item icons.

- InkWell: Wraps a widget to provide a ripple effect and detect touch gestures like onTap.

- SnackBar: Displays a temporary popup message at the bottom of the screen when a card is tapped.

- Custom Widgets (ItemCard, InfoCard): Modular widgets that encapsulate the logic for displaying grid items and information cards, respectively, promoting clean, reusable code.
Additionally, utility widgets like SizedBox, Padding, Center, and MediaQuery are used for responsive layout and spacing.

3. What is the function of the MaterialApp widget? Why is it often the root widget?

The MaterialApp widget in Flutter is the foundation of any app that aims to follow Material Design guidelines. It configures basic app settings such as the theme, routes/navigation, default fonts, and colors. It also initializes the Navigator that manages app routing, handles localization, and ensures proper text direction for different languages. Placing MaterialApp at the root of the widget tree is essential because many child widgets, such as Scaffold, AppBar, and buttons, rely on the Material theme and properties provided by this widget to function properly. Without it, these components may have missing defaults or throw runtime errors.

4. Explain the difference between StatelessWidget and StatefulWidget. When would you choose one over the other?

StatelessWidget and StatefulWidget are the two core building blocks for Flutter UIs. A StatelessWidget is immutable and designed for UI elements that do not change once rendered. It relies entirely on the data provided through constructor parameters and does not store mutable state. Examples include headings, icons, static layouts, and input labels that only need to be drawn once and don't need to react to user events or API changes. In contrast, a StatefulWidget has a companion State class that allows it to maintain and update internal data over its lifecycle using methods like setState(). This makes it suitable for UI components that dynamically respond to interaction or data changes, such as form fields, animations, progress indicators, or data fetched from APIs. As a rule of thumb, start with StatelessWidget for efficiency and simplicity, and convert to StatefulWidget only if mutable state becomes necessary.

5. What is BuildContext and why is it important in Flutter? How is it used in the build method?

BuildContext is a reference object that represents the location of a widget within the widget tree. It provides access to important inherited properties and methods such as those for navigation (Navigator.of(context)), theme colors (Theme.of(context)), layout information (MediaQuery.of(context)), and more. In the build() method, Flutter injects a BuildContext argument, which is then used to retrieve or interact with other widgets higher up in the widget tree. For example, to show a SnackBar, the widget calls ScaffoldMessenger.of(context). This contextual awareness makes BuildContext a powerful tool for designing adaptive, stateful, and navigable UIs.

6. Explain the concept of a “hot reload” in Flutter and how it differs from a “hot restart.”

Hot reload is one of Flutter’s most powerful development features it allows developers to update a running app’s source code and instantly reflect the changes in the UI without losing the app's current state. For example, if you're viewing a counter screen and update the UI style or logic, hot reload applies the change but retains the current counter value. This accelerates UI development and experimentation by dramatically reducing rebuild time. A hot restart, on the other hand, fully resets the Dart VM and reloads the entire app from scratch, including clearing any state variables or interactions. This is often necessary when changes affect the app's global state or when hot reload produces inconsistent behavior. While hot reload is faster, hot restart ensures that the app is fully reinitialized and is often used when debugging issues related to initialization or static configuration.

Assignment 8

1. Explain the difference between Navigator.push() and Navigator.push Replacement() in Flutter. In what context of your application is each best used?

Navigator.push() adds a new page on top of the navigation stack, allowing the user to return to the previous page using the back button. This is best used when the previous page is still relevant, such as navigating from the homepage to a product detail page. Meanwhile, Navigator.pushReplacement() replaces the current page entirely, removing it from the stack so the user cannot go back. This is ideal for flows where returning doesn’t make sense—such as navigating from a login page to the homepage after successful authentication. In my Football Shop app, login → home uses pushReplacement(), while viewing product details uses push().

2. How do you use hierarchy widget like Scaffold, AppBar, dan Drawer to build a consistent page structure in the your application?

Scaffold provides the basic layout architecture of the app, giving consistent structure across all pages. AppBar gives each page a clear title and action buttons in a consistent location, improving navigation clarity. Drawer provides a global navigation menu that can be accessed from any page, ensuring consistent movement across features like product list, add product, and login/logout menu. Together, this widget hierarchy ensures every screen looks unified and follows the same layout pattern.

3. In the context of user interface design, what do you think is the advantages of using layout widget like Padding, SingleChildScrollView, and ListView when displaying form elements? Provide usage examples from your application.

Padding ensures UI spacing is comfortable and readable; without it, elements appear cramped. SingleChildScrollView prevents overflow when forms get long by making the entire content scrollable, which is especially useful for the product creation form. ListView efficiently displays long lists such as the list of product entries because it renders items lazily and scrolls smoothly. These widgets help create a user-friendly interface by improving spacing, readability, and adaptability to screen sizes.

4. How do you set the color theme so that your Football Shop have a visual identity that is consistent with the shop brand.

I set a color theme using ThemeData, defining primary and secondary colors that match the Football Shop’s brand—mainly indigo and white. By configuring this theme at the root MaterialApp, all widgets automatically inherit consistent colors for buttons, app bars, and text. This creates a cohesive visual identity so that every page feels like part of the same brand.

Assignment 9

1. Explain why we need to create a Dart model when fetching/sending JSON data. What are the consequences of directly mapping Map<String, dynamic> without using a model (in terms of type validation, null safety, and maintainability)?

A Dart model enforces strong typing, ensuring that JSON data matches expected types and preventing runtime errors. Without a model, working directly with Map<String, dynamic> becomes error-prone: missing keys, wrong types, or null fields may only cause issues during execution. A model improves readability, maintainability, and guarantees safer data handling, especially when the backend grows.

2. What is the purpose of the http and CookieRequest packages in this assignment? Explain the difference between their roles.

The http package is used for simple stateless API calls that do not require session management (e.g., fetching public data). CookieRequest, however, manages authentication cookies, session state, and CSRF tokens automatically, making it ideal for login, registration, and authenticated requests to Django. In short, http is for generic REST calls, while CookieRequest is specifically for Django session authentication.

3. Explain why the CookieRequest instance needs to be shared across all components in the Flutter application.

CookieRequest stores session cookies and authentication status. If every widget created its own instance, each would lose login state, making the app behave as if the user were logged out. By providing one shared instance via Provider, all pages can access the same logged-in session, allowing secure authenticated communication across the entire app.

4. Explain the connectivity configuration required for Flutter to communicate with Django. Why do we need to add 10.0.2.2 to ALLOWED_HOSTS, enable CORS and SameSite/cookie settings, and add internet access permission in Android? What would happen if these configurations were not set correctly?

Flutter (especially on Android emulator) cannot access localhost, so 10.0.2.2 must be added to ALLOWED_HOSTS. CORS and SameSite/cookie settings allow the browser/emulator to receive Django cookies safely. Android also requires internet permission to access backend APIs. If any configuration is missing, Flutter cannot authenticate, cookies will not be set, or requests will be blocked entirely, resulting in failed login or broken API communication.

5. Describe the data transmission mechanism—from user input to being displayed in Flutter.

User input in Flutter is first collected from form fields, then encoded into JSON and sent through CookieRequest to Django. Django processes the request—validates, stores data in the database, and returns JSON back to Flutter. Flutter decodes this JSON into a Dart model (ProductEntry) and displays the data in widgets such as ListView or cards.

6. Explain the authentication mechanism for login, registration, and logout—from entering account data in Flutter to Django’s authentication process and displaying the menu in Flutter.

For login and registration, Flutter sends user credentials via CookieRequest to Django. Django authenticates using its built-in authentication system, returning a session cookie stored automatically in CookieRequest. All subsequent authenticated requests use that cookie. Logout clears the session on Django and removes the cookie in Flutter. Once logged in, Flutter updates its UI—such as showing personalized menus and user-specific product entries.

7. Explain how you implemented the checklist above step-by-step (not just following a tutorial).

First, I made sure my Django product project was deployable/accessible (at least on localhost), added 10.0.2.2 and my PWS domain to ALLOWED_HOSTS, installed and configured django-cors-headers, and exposed a JSON endpoint that returns my Product model with fields like name, price, description, thumbnail, category, is_featured, and user_id, plus an optional ?filter=mine parameter. On the Flutter side, I defined a custom ProductEntry Dart model that matches that JSON, then set up pbp_django_auth by wrapping MaterialApp with a Provider<CookieRequest> so the same CookieRequest instance is shared across pages. After that, I implemented registration and login screens that call my own Django AJAX views (/auth/register/, /auth/login/) and update the menu and drawer items based on whether request.loggedIn / jsonData indicates a logged-in user. For the product list, I created ProductEntryListPage that fetches data from the JSON endpoint using CookieRequest.get, converts the response into a List<ProductEntry>, and displays it in a ListView using a custom ProductEntryCard widget; tapping a card navigates with Navigator.push to a ProductDetailPage that shows all product attributes. Finally, I implemented the “My Products” filter by adding a toggle button in the list page: when active it either calls the endpoint with ?filter=mine or filters the loaded list in Flutter using product.userId == request.jsonData['id'], tested everything on emulator/browser, and then committed and pushed the changes to GitHub.