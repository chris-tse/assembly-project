	ORG 100
	// ***********************
	// start input routine
	// ***********************
	// get first digit
IN1,SKI
	BUN IN1
	INP

	// add -48 (hex 30) to get actual value
	ADD A

	// store itself to add 9 times
	STA TEN

	// loop to add 9 times
PR,	ADD TEN
	ISZ MUL
	BUN PR

	// store tens value of input
	STA FIR
	// get second digit
IN2,SKI
	BUN IN2
	INP

	// add -48 to get actual value
	ADD A

	// add first digit*10 to second digit
	ADD FIR

	// complement and add 1 to get negative
	CMA
	INC

	// store limit of program negative in LIM
	STA LIM

	// *********************************
	// summing routine
	// *********************************

	// first check if input is 1
	ISZ LIM
	BUN SMR  // go to SumMing Routine
	BUN AOR  // go to Add before Output Routine

	// SumMing Routine loop
SMR,STA LIM 

	LDA SUM     // load sum
	ADD ADR		   // add adder to sum	
	STA SUM        // store sum

	ISZ ADR        
	ISZ ADR        // incrememnt adder x2
	

	LDA LIM  
	INC      // increment limit
	SZA      // check if 0
	SNA      // check if negative
	BUN THC
	INC      // -1
	SZA      // 
	BUN SMR  // 
	BUN THC  //

AOR,LDA SUM
	INC
	STA SUM

THC,LDA SUM  // THousands Counter
	ADD THO
	SPA
	BUN HNC
	ISZ THS
	STA SUM
	BUN THC

HNC,LDA SUM  // HuNdreds Counter
	ADD HUD
	SPA
	BUN TNC
	ISZ HUN
	STA SUM
	BUN HNC

TNC,LDA SUM  // TeNs Counter
	ADD TIN  
	SPA
	BUN ONC
	ISZ TNS
	STA SUM
	BUN TNC

ONC,LDA SUM  // ONes Counter
	ADD UNO
	SPA
	BUN OPR
	ISZ ONS
	STA SUM
	BUN ONC

OPR,LDA THS  // OutPut Routine
	SZA
	BUN 4OPR
	LDA HUN
	SZA
	BUN 3OPR
	LDA TNS
	SZA
	BUN 2OPR
	LDA ONS
	OUT 
	HLT

4OPR,ADD B
	OUT
	LDA HUN
	ADD B
	OUT
	LDA TNS
	ADD B
	OUT
	LDA ONS
	ADD B
	OUT
	HLT

3OPR,ADD B
	OUT
	LDA TNS
	ADD B
	OUT
	LDA ONS
	ADD B
	OUT
	HLT

2OPR,ADD B
	OUT
	LDA ONS
	ADD B
	OUT
	HLT


A,  DEC -48 
B,  DEC 48
TEN,DEC 0	
MUL,DEC -9  // counter for multiplying
FIR,DEC 0	// store first digit * 10
LIM,DEC 0	// used to store negative of input for ISZ looping
SUM,DEC 0	// running sum
ADR,DEC 1	// value to add each round
THS,DEC 0	// thousands counter
HUN,DEC 0	// hundreds counter
TNS,DEC 0	// tens counter
ONS,DEC 0	// ones counter
THO,DEC -1000
HUD,DEC -100
TIN,DEC -10
UNO,DEC -1