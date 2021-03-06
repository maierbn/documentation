.. Coding standard for contributing to OpenCMISS

===============
Coding Standard
===============

.. contents::


General comments
----------------

* Generally, try to ensure that new code is consistent in formating, style, look and feel and convention with existing code. If in doubt about whether or not a new coding style rule is required please raise the issue rather than adopt a new style. 
* Be professional in your coding style, comments, error messages, layout and other output. Avoid attempts at humour etc.

Code Comments
-------------

* Do not comment out code changes with dates and initials. The code management system will record all changes and who changed what and when.
* All new code should be properly commented and describe what the code does, why it was added and (if appropriate) describe any limitations.
* Do not use comments as an excuse for poor code. 
* If you implement an algorithm from a paper or book put a reference to the source in the comments.

=======================
Fortran Coding Standard
=======================

Code Layout
-----------

* Free source form **must** be used.
* A double space should be used for an indent. Tabs **must not** be used anywhere in the code.
* Code should have no more than ``132`` characters in a line, use continuation ``&`` 's if need be. There should be a space before the first continuation character and a space after the second continuation character when continuing lines. Continuation lines should be indented by ``2`` spaces with respect to the first line.
* All arguments to a ``SUBROUTINE/FUNCTION`` must be declared with one variable per line. Doxygen comments must be used to document the variable usage. If a variable is to be changed/returned by the ``SUBROUTINE/FUNCTION`` indicate this in the doxygen comment *e.g.*, ``INTEGER(INTG), INTENT(OUT) :: numberOfNodes !<On return, the number of nodes in the basis.``
* When commenting array variables in doxygen, include in the doxygen comment information about the array indicies *e.g.*, ``INTEGER(INTG), ALLOCATABLE :: numberOfDerivatives(:) !<numberOfDerivatives(localNodeIdx). The number of derivatives at the localNodeIdx'th local node in the basis``.
* When commenting variables that are associated with a list of parameters a reference should be map in the doxygen comment to the doxygen description of those parameters *e.g.*, ``INTEGER(INTG) :: type !<The type of the field. \see FieldRoutines_FieldTypes``
* In general, code routines, local variable lists etc. should be alphabetical.
* ``CASE`` keyword in a ``SELECT CASE`` statement should have the same indentation as the ``SELECT`` statement. The contents of the ``CASE`` statement should be indented by ``2`` spaces.
* Add whitespace where appropriate to improve readability.
* Use a ``!================``... marker between subroutines and functions.

Case Style
----------

* Constants should be in all capitals with underscores between words, *e.g.*, ``SOME_CONSTANT_VALUE``.
* Routine parameters and variables, type components should be in lower camel case, *e.g.*, ``lowerCamelCase``.
* Types, routines and class methods should be in upper camel case, *e.g.*, ``UpperCamelCase``.
* Where a routine is to be a method of a class in bindings to an object oriented language, or could be thought of as a method of a type in internal code, the method name and type name should be separated by an underscore, *e.g.*, ``Basis_NumberOfXiGet``.
* Fortran key words and intrinsic functions should be in upper case.

Fortran code
------------

* ``IMPLICIT NONE`` **must** be used in all modules and programs.
* ``INTENT(IN|OUT|INOUT)`` must be used for all dummy arguments including pointers. 
* If there is just a single statement following an ``IF`` clause use the inline form of the ``IF`` statement and do not use ``THEN`` and ``END IF``.
* For dummy array arguments the dimension qualifier should be with the array name *i.e.*, use ``INTEGER(INTG) :: fred(N)`` rather than ``INTEGER(INTG), DIMENSION(N) :: fred``.
* Always name program units, types and interfaces and use the corresponding ``END PROGRAM``, ``END SUBROUTINE``, ``END MODULE``, ``END TYPE``, ``END INTERFACE`` etc. etc. 
* Never use a Fortran keyword as a variable name. Never use the name of an intrinsic function as the name for a user-defined function.
* Use ``::`` after the declaration part of a variable, even if there are no attributes.
* All explicit constants should have the kind attribute at the end *i.e.*, ``3.14159_DP`` rather than ``3.14159``.
* Declare the length of character variables with ``CHARACTER(LEN=xxx)``. 
* Use ``[]`` array constructors rather than ``/( )/``.
* All variable decalarations involving a base type must always be qualified with a ``KIND`` selection *e.g.*, ``REAL(DP) ::`` rather than ``REAL ::``.
* Use the relational operators ``<``, ``>``, ``<=``, ``>=``, ``==`` and ``/=`` rather than ``.LT.``, ``.GT.``, ``.LE.``, ``.GE.``, ``.EQ.`` and ``.NE.``
* Use array syntax whenever possible *e.g.*, ``A=B`` instead of ``A(:)=B(:)``
* Use assumed shape arrays where ever possible *i.e.*, ``A(:)`` instead of ``A(*)`` for array arguments.
* No space between the conditional statement and condition *i.e.*, ``IF(`` rather than ``IF (``, ``WHILE(`` rather than ``WHILE (`` etc.
* All multiword Fortran statements should have a space *i.e.*, ``END IF``, ``ELSE IF``, ``END DO``, ``END SELECT`` etc.
* For read/write/print statement, avoid the comma before the data variable *e.g.*, use ``READ(filedId, CHAR(dpFmt), IOSTAT=ios) realData(1:lenOfData)`` instead of ``READ(fileId, CHAR(dpFmt), IOSTAT=ios), realData(1:lenOfData)``
* In an ``IF/WHILE`` statement, do not use full logical expressions *e.g.*, use ``IF(someValue)`` or ``IF(.NOT.someValue)`` instead of ``IF(someValue==.TRUE.)`` or ``IF(someValue==.FALSE.)``
* Do not use multiple statements in one line. Use separate lines for each statement.
* An ``INTERFACE`` block must be used for all ``SUBROUTINES/FUNCTION`` s that are not otherwise automatically available via a ``USE`` statement and ``MODULE`` s.
* ``SELECT CASE`` statements must always have a ``CASE DEFAULT`` clause. If there is no default action include the ``CASE DEFAULT`` and put ``!Do nothing as a comment``.

Fortran features to be avoided
------------------------------

* ``COMMON`` blocks - use ``MODULE`` instead
* ``EQUIVALENCE``
* Assigned and computed ``GOTO`` s - use ``SELECT CASE`` statements
* Artihmetic ``IF`` statements - use a full ``IF``, ``ELSE IF``, ``ELSE``, ``END IF`` or ``SELECT CASE`` instead. 
* ``GOTO`` and ``CONTINUE`` - use ``IF``, ``CASE``, ``DO WHILE``, ``EXIT`` and ``CYCLE`` instead.
* ``PAUSE`` statements
* ``ENTRY`` statements
* ``DATA`` and ``BLOCK DATA``
* Implicitly changing the shape of an array when passing it into a subroutine.

Allowed Fortran features
------------------------

Fortran 90
^^^^^^^^^^

* All features.

Fortran 95
^^^^^^^^^^

* All features.

Fortran 2003
^^^^^^^^^^^^

* C interoperability. Use C types for the interface only. Internal code should use Fortran types.
* Access to the computing environment.
* ISO TR 15581 allocatable enhancements.
* ``[]`` array constructors.
* Pointer intents.
* ``MOVE_ALLOC``

Fortran 2008
^^^^^^^^^^^^

* No features at this stage.

Fortran 2015
^^^^^^^^^^^^

* No features at this stage.

Dynamic memory
--------------
 
* Automatic arrays (*i.e.*, those arrays declared within a ``SUBROUTINE/FUNCTION`` using the size of an input argument) are preferred over ``ALLOCATABLE`` and ``POINTER`` arrays.
* ``ALLOCATABLE`` arrays are preferred over ``POINTER`` arrays unless full pointer functionality is required.
* All memory allocations should check to see if the allocation was successful and flag an error if not.
* All pointers/allocated memory should be checked to see if they are ``ASSOCIATED/ALLOCATED`` before de-referencing/using them.
* All pointers should be checked to ensure that they are not associated before allocation.
* All dynamically allocated variables in a routine should be deallocated on the exit from a routine under error conditions.

Code conventions
----------------

* Use fully spelt out variable names unless abbreviations are required to avoid maximum identifier length problems.
* Use standard loop variable names *e.g.*, ``localNodeIdx``, ``componentIdx``, when looping rather than temporary variable names.
* The first arguement to routines should be the object the routine is operating on, except for ``xxx_CreateStart`` routines, where the created object must be the last parameter.
* All ``TYPE`` s shall have ``xxx_Initialise`` and ``xxx_Finalise`` routines for construction and destruction.
* Within a module all named constants and procedure names should be prefixed by a name indicating that module so as to maintain a namespace.
* Use DOF/node hierarchy consistently in subroutine calls. *i.e.*, ``versionNumber,derivativeNumber,nodeNumber,componentNumber`` instead of reverse order.
* For subroutine arguments the input variables should be first, then the output variables and then the error variables. Variables should, in general, be arranged alphabetically unless another coding convention dictates otherwise (*e.g.*, DOF/node hierarchy).
* If variables are out of range then any error messages should try to provide information on what variables are out of range and what the values are.
* **Do not** use temporary write statements for debugging or other purposes. Use diagnostics. If the values of the variables are of importance to you for working out how the routine works then they will be of importance to others at a later time and thus time should be taken to provide detailed diagnostic output. 
* For routines that return information (*i.e.*, get routines) use ``SUBROUTINE`` instead of ``FUNCTION``. The result should be returned in memory supplied by the calling routine. The size of the supplied memory should be checked to ensure that it is large enough to hold the result. 
* When using case statements put in all known values of the the case variable and use a ``CALL FlagError("Not implemented.",`` ... statement for the cases that are not yet implemented.
* As OpenCMISS needs to be used as a wrapped library all output should have the ability to be turned on or off. The default behaviour is that all output should be off. 
* All output should be through the input/output routines. **No output** should be written out via ``WRITE`` or ``PRINT`` statements.

Good practice
-------------

* All compiler warnings (*e.g.*, unused variables) should be removed before committing code. Persistent compiler warnings can mask a new genuiue compiler warning leading to bugs.
* All error messages should be a proper sentance (with a full stop).
* Input arguments should be checked in a subroutine before being used.
* All pointer arguments that are assigned within a routine should be checked to ensure that they are ``NULL`` on entry.
* All constants should be declared as named parameters. Never hardcode a constant in the code.

Pre-processing
--------------

* Pre-processing for file inclusion and conditional compilation are allowed. 

Sample module
-------------

.. code-block:: fortran

   !> \file
   !> \author xxx
   !> \brief This module handles all problem routines.
   !>
   !> \section LICENSE
   !>
   !> Version: MPL 1.1/GPL 2.0/LGPL 2.1
   !>
   !> The contents of this file are subject to the Mozilla Public License
   !> Version 1.1 (the "License"); you may not use this file except in
   !> compliance with the License. You may obtain a copy of the License at
   !> http://www.mozilla.org/MPL/
   !>
   !> Software distributed under the License is distributed on an "AS IS"
   !> basis, WITHOUT WARRANTY OF ANY KIND, either express or implied. See the
   !> License for the specific language governing rights and limitations
   !> under the License.
   !>
   !> The Original Code is OpenCMISS
   !>
   !> The Initial Developer of the Original Code is University of Auckland,
   !> Auckland, New Zealand and University of Oxford, Oxford, United
   !> Kingdom. Portions created by the University of Auckland and University
   !> of Oxford are Copyright (C) 2007 by the University of Auckland and
   !> the University of Oxford. All Rights Reserved.
   !>
   !> Contributor(s):
   !>
   !> Alternatively, the contents of this file may be used under the terms of
   !> either the GNU General Public License Version 2 or later (the "GPL"), or
   !> the GNU Lesser General Public License Version 2.1 or later (the "LGPL"),
   !> in which case the provisions of the GPL or the LGPL are applicable instead
   !> of those above. If you wish to allow use of your version of this file only
   !> under the terms of either the GPL or the LGPL, and not to allow others to
   !> use your version of this file under the terms of the MPL, indicate your
   !> decision by deleting the provisions above and replace them with the notice
   !> and other provisions required by the GPL or the LGPL. If you do not delete
   !> the provisions above, a recipient may use your version of this file under
   !> the terms of any one of the MPL, the GPL or the LGPL.
   !>

   !> This module handles all problem routines.
   MODULE Sample

     USE Xxx

   #include "macros.h"

     IMPLICIT NONE

     PRIVATE

     !Module parameters

     !Module types

     !Module variables

     !Interfaces

   CONTAINS

     !
     !==================================================================================================================================
     !

     !>Subroutine description.
     SUBROUTINE DoSomething(input,output,err,error,*)

       !Argument variables		
       INTEGER(INTG), INTENT(IN) :: input !<Input variable description.
       INTEGER(INTG), INTENT(OUT) :: output !<On return, the output variable description.
       INTEGER(INTG), INTENT(OUT) :: err !<The error code
       TYPE(VARYING_STRING), INTENT(OUT) :: error !<The error string
       !Local Variables

       ENTERS("DoSomething",err,error,*999)


       EXITS("DoSomething")
       RETURN
   999 ERRORS("DoSomething",err,error)
       EXITS("DoSomething")
       RETURN 1
   
     END SUBROUTINE DoSomething
  
     !	      
     !==================================================================================================================================
     !

     !>Function description.
     FUNCTION DoSomethingElse(input,output,err,error)

       !Argument variables		
       INTEGER(INTG), INTENT(IN) :: input !<Input variable description.
       INTEGER(INTG), INTENT(OUT) :: output !<On return, the output variable description. Should rarely be used - use the function variable instead in possible.
       INTEGER(INTG), INTENT(OUT) :: err !<The error code
       TYPE(VARYING_STRING), INTENT(OUT) :: error !<The error string
       !Function variable
       INTEGER(INTG) :: DoSomethingElse
       !Local Variables

       ENTERS("DoSomethingElse",err,error,*999)


       EXITS("DoSomethingElse")
       RETURN
   999 ERRORSEXITS("DoSomethingElse",err,error)
       RETURN
   
     END FUNCTION DoSomethingElse
        
     !
     !==================================================================================================================================
     !

   END MODULE Sample

=====================
C/C++ Coding Standard
=====================

** coming soon
