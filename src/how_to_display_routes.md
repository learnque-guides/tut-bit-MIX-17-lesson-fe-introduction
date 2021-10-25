# How to display routes?

Angular has separate tags designed for displaying the route:

```html
<h1>Main Page</h1>
<nav>
    <a routerLink="/test" routerLinkActive="active">Test Page</a>
    <a routerLink="/test2" routerLinkActive="active">Test Page 2</a>
</nav>
<router-outlet>
    { OUR COMPONENT UNDER THE ROUTER WILL BE DISPLAYED HERE }
</router-outlet>
```

Basically, all content that should differ from page to page like page content, details, etc. should go inside router-outlet tag. Content that does not change like navigation, header or footer should stay outside.
