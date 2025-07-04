# Automatic Repair Method for Null Pointer Dereferences Guided by Program Dependency Graph

Year: 2022

Link: https://www.mdpi.com/2073-8994/14/8/1555

## Notes: 

* PDG (Program Dependency Graph) accurately describes both data dependencies and control dependencies within a program. 
  * PDG uses data dependencies (based on the analysis of variable dependencies) and control dependencies (based on the the post-dominanc relation among statements in the control flow graph)

* Similar to VFix, it uses value flow analysis to identify the root cause of NPE.

* Four repair mechanisms are proposed:
  * assignment mechanism - assigns an appropriate value to the faulty pointer at the source of the defect whenever possible
  * restraint mechanism - sets up a simple check to bring an affected scope by the defect into the safe scope
  * evading mechanism - changes the execution of the program to avoid null pointer dereferences
  * transfer mechanism - throws an exception to the caller of the method that contains the defect and catches it there

* Repair process is as follows:
  * firstly, the defect variable, the defect start line, and the defect end line are acquired by a defect detection tool
  * the control dependency graph and data dependency graph are obtained by employing static analysis
  * the result of the first two steps are combined to generate the PDG to receive the complex dependencies in a program
  * different repair mechanisms are implemented to generate candidate patches for inter-procedural and intra-procedural null pointer dereferences