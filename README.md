# AngularJS Secure Code Review Guide

Expressions are evaluated against the scope of the corresponding controller
- allows for writing a subset of javascript

Directives are markers for enriching HTML with custom functionallity 

// Directive as a tag
<person name="expression"></person>

// Directive as an attribute
<div person name="expression"></div>

Coding Principles: 
- Manual output encoding in a complex project is doomed to fail (too complex)!


How Strict Contextual Auto Escaping works....
...within the controller...
$scope.url = <user-controlled>;
 
...within the view....
 <!-- url gets auto-encoded and validated -->
  <iframe = ng-src="{{url}}"></iframe>

  what does ng-bind-html do?
  - sanitizes all JS from the HTML  string (just like DOM purify)

Types of Security Bugs for AngularJS Apps:
  SSTI (Server-Side Template Injection)
    Angular is Client-side framework....
    - logic is all implemented in JS
    - Server is the mechanism to store data and code
    - Server must not generate temples based on user input
    
    ANY TEMPLATE RECEIVED FROM THE SERVER IS CONSIDERED TRUSTED
  
    Pitfall #1: php htmlentities does not support "expressions" (it doesn't know how {{}} will be treated)
  
    We could write any expression and have it execute within the scope of the controller....
    Most big apps have a lot of functionality which an attacker could use to do harm.... {{deleteUserAccount()}}
  
  
Code Smells: 
  Is there.... 
  
  Unsafe Assignment of DOM Elements?
  -  Binding with "...innerHTML = untrustedData"?
  
  
  Untrusted Input assigned directly to DOM element via an angular.element
  -  Developer needs to sanitize input prior to leveraging this Angular JQuery'ish assignment 

  Server-Side Template Injection?
    - Are templates being created dynamically server-side where an attacker could inject a malicious expression which would then execute under 
    the client's context?
  
  Sandbox Escapes?
  
Automated Detection using a Linter:
https://github.com/LewisArdern/eslint-plugin-angularjs-security-rules/tree/master/tests/rules 



Types of Vulnerabilities and How To Exploit Them: 

Mixed Context: HTML + URL 
<?php 
  echo "<a href = " . encodeForHTML(validateUrl($_GET['url'])) . ">link</a>;
?>
^ this is vuln to XSS since we know href attributes support JavaScript URL's 
This allows for an attacker to write javascript:alert(1) and still be successful







Options to Exploit:

Depending on version, Sandbox 

What is the ng-non-bindable directive?
This tells AngularJS to not compile or bind contents of the curr DOM element - allows for them to be displayed but not processed 


Old-Skool AngularJS? 
- In versions prior to version 1.2, devs needed to use the ng-bind-html-unsafe directive to invoke the Strict Contextual Escaping protection mechanism 

Exercises to Practice Your Skillz!

BUGPOC XSS Challenge: 
- https://arwildo.medium.com/injects-a-dom-based-xss-on-angular-app-bugpoc-2020-xss-challenge-e88b1ff221e

God-tier Resources:
https://owasp.org/www-pdf-archive/Benelus_day_20161125_S_Lekies_Securing_AngularJS_Applications.pdf <- Amazing code examples (how to do things correctly & incorrectly)

Resources:
https://owasp.org/www-chapter-london/assets/slides/OWASPLondon20170727_AngularJS.pdf
https://blog.nvisium.com/angular-for-pentesters-part-1
https://blog.nvisium.com/angular-for-pentesters-part-2

Best Practice Docs:
https://angularcodereview.com/angularjs/



