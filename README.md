# AngularJS Secure Code Review Guide


Code Smells: 
  Is there 


Options to Exploit:

Depending on version, Sandbox 

What is the ng-non-bindable directive?
This tells AngularJS to not compile or bind contents of the curr DOM element - allows for them to be displayed but not processed 


Old-Skool AngularJS? 
- In versions prior to version 1.2, devs needed to use the ng-bind-html-unsafe directive to invoke the Strict Contextual Escaping protection mechanism 



Resources:
https://owasp.org/www-chapter-london/assets/slides/OWASPLondon20170727_AngularJS.pdf
