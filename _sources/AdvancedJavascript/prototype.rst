Javascript Prototypes
=====================


Object Creation
---------------

.. activecode:: proto_1
   :language: javascript
   
   x  = Object.create(null)
   x.foo = 1
   x.bar = 2
   alert(x['bar'])
   
   
   


To try:


.. code-block:: javascript

   x = Object.create(null)
   x.bar = 1
   x.foo = function() {
       console.log(this.bar)
   }
   x.foo()


   y = Object.create(x)
   y.foo()
   y.bar=2
   y.foo()


   z = function() {
       this.bar = 2
       this.foo = function() {
           console.log(this.bar)
       }
       return this
   }

   z1 = z()
   z1.foo()

   myClass = function() {
       this.bar = 22
       this.foo = function() {
           console.log(this.bar)
       }
   }

   z2 = new myClass()
   z2.foo()
   console.log(z2.prototype)


   MyClass = function(x,y,z) {
   	var priv = x
   	this.pub = y
   	//if (z == undefined) {
   	//	z = 'default value'
   	//}
   	this.something = z

   	var innerFunc = function() {
   		priv = priv + 1
   	}

   	this.publicFunction =function(z) {
   		priv = priv + z
   		return priv
   	}

   }

   MyClass.prototype.outerfunction = function(a) {
   	this.pub = this.pub + a
   	//priv = priv + 1
   	return this.pub
   }

   foo = new MyClass(10,20,30)
   console.log(foo.outerfunction(99))
   console.log(foo.publicFunction(99))
   //foo.innerFunc()
   



Exercise
--------

Create a Person class, they should have private ivars for ssn and weight.  public ivars for age and name.
public methods for gainWeight, getSSN, and getWeight.
add a prototype method for birthday that adds one to the age, and also returns the new age.


.. actex:: proto_person
   :language:  javascript
   
   // your code here
   
   