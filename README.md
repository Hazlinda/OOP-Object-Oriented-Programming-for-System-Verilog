# OOP-Object-Oriented-Programming-for-System-Verilog

# Inheritance

It is a mechanism where you can to derive a class from another class for a hierarchy of classes that share a set of attributes and methods. Normally for first class we created it known as Parent class, the next class created will known as child class. To extends both class we called as inherit. Using extends keyword we inherit the class. 

In heritance they have 5 type:
1. 
2.
3.
4.
5.

        //////////////////////////////////////////
        //Examples show Inheritance Polymorphism//
        //////////////////////////////////////////
        
        module top ();

        class base;
            virtual function void my_task (); //parents class have their own properties and method
                $display ("This is base_class");
            endfunction
        endclass

        //////////////////////////////////////
        //This is Extend class (child class)//
        //////////////////////////////////////
        
        class ext_class extends base;   //child class inheriting with class parent
            function void my_task ();     //child class inherit all the properties and method from parents class 
                $display ("This is extended class");
            endfunction
        endclass

        base bs_hand;  //create the handle for both class
        ext_class ex_hand;

            initial begin   
                bs_hand = new;   
                ex_hand = new;
                bs_hand.my_task ();  //access by 
                $display ("\n Applying polymorphism:Overriding base-class method by extended class \n");
                bs_hand = ex_hand; // Here polymorphism is done.
                bs_hand.my_task ();
            end
        endmodule  


# Abstraction

Abstraction is nothing but its show only necessary

        ///////////////////////////
        //Examples of ABSTRACTION//
        ///////////////////////////
        
        module top();

            virtual class base;  //Declaring a virtual calss creates a abstract class template that MUST be extended
                function void run ();
                    $display("Running Base");
                endfunction
                pure virtual function void play();
            endclass

        class child extends base;
                function void run ();
                    $display("Running Child");
                endfunction

            virtual function void play();
                $display("Playing football");
            endfunction
        endclass

        child c;
            initial
            begin
                c = new;
                c.run ();
                c.play();
          end
     endmodule

V C S   S i m u l a t i o n   R e p o r t 

Running Child
Playing football
           


# Encapsulation

Hiding the properties from being accessed outside the class. 
Use protected keyword, if we want to make the properties accessible in the extended classes (but not outside the classes or main program). 

In systemverilog, two keywords are specified to hide a class member.

1. local
This will ensure that the member is available only to the method of the same class. Even, a local member will not be available to its extended classes.

2. protected
If we want to make the properties accessible in the extended classes but not outside the classes. We can declare the properties as protected.

Example:

    //////////////////////////////////////////////////////////////////////
    // Example of Encapsulation using string local and protected keyword//
    //////////////////////////////////////////////////////////////////////
    
    class base;
        string my_public;
        local string my_local;
        protected string my_protected;
  
        function new();
            my_public = "FOR ALL";
            my_local = "FOR BASE ONLY";
            my_protected = "EXTENDED CLASS CAN USE";
        endfunction

        task print();
            $display();
            $display ("BASE class: my_public = %0s",my_public);
            $display ("BASE class: my_local = %0s",my_local);
            $display ("BASE class: my_protected = %0s\n",my_protected);
        endtask
    endclass

    //////////////////////////////////////
    //This is Extend class (child class)//
    //////////////////////////////////////
    
    class extended extends base;

        task print();
            $display ("EXTENDED class: my_public = %0s",my_public);
            //$display ("extended class: my_local = %0s",my_local);
            // Above commented line will give compile error: Illegal class variable access. because its local to base only
            $display ("EXTENDED class: my_protected = %0s \n",my_protected);
        endtask
    endclass

    ///////////////////////////////////////
    //This is Distinct class (new class)/// 
    ///////////////////////////////////////
    
    class distinct;
        base b=new();  //object created 

        task print();
            $display ("DISTINCT class: my_public = %0s\n",b.my_public);
            //$display ("distinct class: my_local = %0s",b.my_local);
            //$display ("distinct class: my_protected = %0s",b.my_protected);
            // Above both commented line will give compile error: Illegal class variable access. because local and protected properties can’t be accessed from outside class
        endtask
    endclass

    //////////////////
    //Program start/// 
    //////////////////
    
    program encapsulation;
        base b=new();  //object create
        extended ex=new();
        distinct dis=new();

      initial begin
        b.print();
        ex.print();
        dis.print();
      end
    endprogram

V C S   S i m u l a t i o n   R e p o r t

BASE class: my_public = FOR ALL
BASE class: my_local = FOR BASE ONLY
BASE class: my_protected = EXTENDED CLASS CAN USE

extended class: my_public = FOR ALL
extended class: my_protected = EXTENDED CLASS CAN USE 

distinct class: my_public = FOR ALL

       

In system verilog all the properties of the class are public by default or we can say it can be accessed outside the class directly using the dot operator. If we want to protect the access of the class variables/properties from outside the class we can use the local keyword.

  
# Polymorphism

Poly means Many and Morphism means forms
Polymorphism is more than one function with same name, but have different working (One thing can be represent in many form)

Two type of Polymorphism
1. Compile time 
2. Run time 

        ////////////////////////////
        //Examples of Polymorphism//
        ////////////////////////////
        module top ();

        class base;
	        function void my_task ();
  	        $display ("This is base_class");
	        endfunction
        endclass

        class ext_class extends base;//Here inheritance is applying
	        function void my_task ();
	        $display ("This is extended class");
	        endfunction
        endclass

	        base base_hand;
	        ext_class ext_hand;

	        initial begin
	        base_hand = new;
	        ext_hand = new;
                     base_hand.my_task ();
		        $display ("\n Applying polymorphism:Overriding base-class method by extended class \n");
		        base_hand = ext_hand; // Here polymorphism is done 
		        base_hand.my_task ();
	        end
        endmodule
