# Testing AngularJS Directives
### beforeEach Setup
```
var $compile;
var $rootScope;
var expectedHtml = 'some html';

beforeEach(module('MyApp'));

beforeEach(inject(function(_$rootScope_, _$compile_){
    $rootScope = _$rootScope_;
    $compile = _$compile_;
}));
```
### beforeEach Setup For Using templateUrl
```
beforeEach(inject(function($templateCache){
    var template = null;

    var req = new XMLHttpRequest();
    req.onload = function(){
        template = this.responseText;
    };

    req.open("get", "template.thml", false);
    req.send();

    $templateCache.put("template.html", template);
}));
```
### Test Method
```
it('should property insert content', function(){
    var item = {name: "John"};
    $rootScope.item = item;

    var html = "<my-directive item='item'></my-directive>";

    var elem = $compile(html)($rootScope);

    $rootScope.$digest();

    expect(elem.html()).toContain(expectedHtml);
});
```