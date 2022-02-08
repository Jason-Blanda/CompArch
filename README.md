module Lab2 (clock, reset,I, st_out, F);
input   clock,reset,I;
output  reg [2:0]st_out;
output reg F;

parameter S0  = 3'b000,S1 = 3'b001,S2 = 3'b010,S3 = 3'b011,S4 = 3'b100 ;
reg   [2:0]          state        ;
reg   [2:0]          next_state   ;

always @ (posedge clock)

begin : FSM
if (reset == 1'b1) begin
state <=  S0;
st_out <= 3'b000;
F <= 0;
end else
case(state)
S0 : if (I == 1'b1) begin
next_state <=  S1;
st_out <= 3'b001;
F <= 0;
end 
else if (I == 1'b0) begin
next_state <=  S0;
st_out <= 3'b000;
F <= 0;
end 
else begin
    st_out <= 3'b000;
F <= 0;
  end
S1 : if (I == 1'b0) begin
next_state <=  S2;
st_out <= 3'b010;
F <= 0;
end 
else if (I == 1'b1) begin
next_state <=  S1;
st_out <= 3'b001;
F <= 0;
end 
else begin
    st_out <= 3'b001;
F <= 0;
end
S2: if (I == 1'b0) begin
next_state <= S3;
st_out <= 3'b011;
F <= 0;
end
else if ( I == 1'b1) begin
next_state <= S1;
st_out <= 3'b001;
F <= 0;
end
else begin
	st_out <= 3'b010;
F <= 0;
end
S3: if (I == 1'b1) begin
next_state <= S4;
st_out <= 3'b100;
F <= 1;
end
else if (I == 1'b0) begin
next_state <= S0;
st_out <= 3'b000;
F <= 0;
end
else begin
	st_out <= 3'b011;
F <= 0;
end
S4: if (I == 1'b0) begin
next_state <= S0;
st_out <= 3'b000;
F <= 0;
end
else if (I == 1'b1) begin
next_state <= S2;
st_out <= 1'b010;
F <= 0;
end
else begin
	st_out <= 3'b100;
F <= 1;
end
default : state <=  S0;
endcase
end
endmodule // End of Module arbiter
