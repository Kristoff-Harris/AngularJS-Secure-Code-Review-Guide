# AngularJS Secure Code Review Guide


Code Smells: 
  Is there 
  
  Unsafe Assignment of DOM Elements?
  -  Binding with "...innerHTML = untrustedData"?
  
  
  Untrusted Input assigned directly to DOM element via an angular.element
  -  Developer needs to sanitize input prior to leveraging this Angular JQuery'ish assignment 

  Server-Side Template Injection?
  
  Sandbox Escapes?
  
Automated Detection using a Linter:
https://github.com/LewisArdern/eslint-plugin-angularjs-security-rules/tree/master/tests/rules 







Options to Exploit:

Depending on version, Sandbox 

What is the ng-non-bindable directive?
This tells AngularJS to not compile or bind contents of the curr DOM element - allows for them to be displayed but not processed 


Old-Skool AngularJS? 
- In versions prior to version 1.2, devs needed to use the ng-bind-html-unsafe directive to invoke the Strict Contextual Escaping protection mechanism 

Exercises to Practice Your Skillz!

BUGPOC XSS Challenge: 
- https://arwildo.medium.com/injects-a-dom-based-xss-on-angular-app-bugpoc-2020-xss-challenge-e88b1ff221e

Resources:
https://owasp.org/www-chapter-london/assets/slides/OWASPLondon20170727_AngularJS.pdf
https://blog.nvisium.com/angular-for-pentesters-part-1
https://blog.nvisium.com/angular-for-pentesters-part-2

