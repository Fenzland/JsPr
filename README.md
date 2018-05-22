JsPr
================================

A JS module to hack private member of JS object.

## Usage

```js
import makeJsPr from './path-to-jspr/main.js';

const { _, $, }= makeJsPr();

class Foo
{
	constructor( pub, pri, )
	{
		this.pub= pub;
		
		// access to a private property
		_(this).pri= pri;
		
		// call a private method
		_(this).init();
	}
}

// define a private method
_(Foo.prototype).init= function(){
	
	// access to a private property in private method
	this.pri;
	
	// access to a public property in private method
	$(this).pub;
};

// if you don't like _ and $
const { _:toPrivate, $:toPublic, }= makeJsPr();

```

Each time `makeJsPr()` called, a brand new specific pair of `{ _, $, }` created, with a stand alone private scope.
Keep this pair safely, because they are the key of the world of your private members.


## Relation of objects

```js

// if you don't like logic, forgive this.

const foo= new Foo();

_(foo) instanceof _(Foo);
_(foo).constructor === _(foo.constructor) === _(Foo);
_(foo).__proto__ === _(foo.__proto__) === _(Foo).prototype === _(Foo.prototype);

const _foo= new (_(Foo))();

_foo instanceof _(Foo);
$(_foo) instanceof Foo;
$(_foo).constructor === $(_(Foo)) === Foo;
$(_foo).__proto__ === $(_foo.__proto__) === $(_(Foo).prototype) === Foo.prototype

```
