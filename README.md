# OOP-Object-Oriented-Programming-for-System-Verilog

# Abstraction



# Encapsulation

In system verilog all the properties of the class are public by default 
or we can say it be accessed outside the class directly using the dot operator. 
If we want to protect the access of the class variables/properties from outside the class we can use the local keyword. 
Hiding the properties from being accessed outside the class is called encapsulation. If we want to make the properties accessible in the extended classes but not outside the classes. We can declare the properties as protected. 
Then it will be available in the extended classes but not in the main program.

In systemverilog, two keywords are specified to hide a class member.

local: This will ensure that the member is available only to the method of the same class. Even, a local member will not be available to its extended classes.
protected: If we want to make the properties accessible in the extended classes but not outside the classes. We can declare the properties as protected.

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
    //This is Distinct class (new class)// 
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

$finish at simulation time                    0
           


  
