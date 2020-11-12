# Checklist for Code Reviews

* [ ] **Issue Tracker Hygiene (Jira, Redmine etc.)**
    * [ ] Is the fix version set?
    * [ ] Are the necessary sub tasks completed?
    * [ ] Are issue specific CoS satisfied?
* [ ] **Code Quality**
    * [ ] Are there any potential NPEs?
    * [ ] Are variable, class and method name easily understandable?
    * [ ] Are there any Service/EJB gotchas?
        * [ ] Persistent class variables that aren't cleared when a method is called?
* [ ] **Business Logic**
    * [ ] Do you understand what the business logic/requirements behind the code?
    * [ ] Is complicated business logic covered by JavaDocs/comments?
* [ ] **Testing**
    * [ ] Are there any new public methods/classes that need to be tested?
    * [ ] Are failure & special cases covered?
    * [ ] Does the test name adequately explain the test case?
    * [ ] Is the test easily readable and maintainable?


