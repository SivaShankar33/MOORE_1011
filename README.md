# MOORE_1011
# State Diagram
![image](https://github.com/RESMIRNAIR/MOORE_1011/assets/154305926/4c056127-254f-4b9a-88d1-5486b2577ba3)
# Program 
Module Sequence_Detector_Moore(clock,reset,sequence_in,detector_out);
input clock, reset, sequence_in; 
output reg detector_out; 
parameter  S0=3'b000,S1=3'b001,S2=3'b010,S3=3'b011,S4=3'b100;
reg [2:0] current_state, next_state; 
always @(posedge clock, posedge reset)
begin
 if(reset==1) 
 current_state <= S0;
 else
 current_state <= next_state; 
end
always @(current_state,sequence_in)
begin
 case(current_state) 
 	S0:begin
		if(sequence_in==1)
   			next_state = S1;
  		else
   			next_state = S0;
 	   end
 	S1:begin
  		if(sequence_in==0)
   			next_state = S2;
  		else
   			next_state = S1;
 	   end
    S2:begin
  	if(sequence_in==0)
   		next_state = S0;
 	 else
   		next_state = S3;
    end 
  S3:begin
  	if(sequence_in==0)
   		next_state = S2;
  	else
   		next_state = S4;
     end
  S4:begin
  	if(sequence_in==0)
   		next_state = S2;
  	else
   		next_state = S1;
    end
 	default:next_state = S0;
endcase
end
always @(current_state)
begin 
 case(current_state) 
 	S0:   detector_out = 0;
 	S1:   detector_out = 0;
 	S2:  detector_out = 0;
 	S3:  detector_out = 0;
 	S4:  detector_out = 1;
 	default:  detector_out = 0;
 endcase
end 
endmodule
# Output:
![image](https://github.com/SivaShankar33/MOORE_1011/assets/125188331/2429164d-3a22-4d88-8ebb-45520f0912dd)
