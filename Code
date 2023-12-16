# ProjectCode

module Project (
input clk,
input rst,
input [7:0]in,
input en_a,
input sel_a_path,
input en_b,
input sel_b_path,
input en_c,
input [2:0]alu_control, 
input [1:0]val_to_display,
output [6:0]seg7_neg_sign,
output [6:0]seg7_dig0,
output [6:0]seg7_dig1,
output [6:0]seg7_dig2
);

reg [7:0] seg7_val;
reg [7:0] temp_a;
reg [7:0] temp_b;
wire [7:0] temp_c;

wire [7:0] a;
wire [7:0] b;
wire [7:0] c;

three_decimal_vals_w_neg three_d(seg7_val, seg7_neg_sign, seg7_dig0, seg7_dig1, seg7_dig2);

register a_reg(clk, rst, temp_a, en_a, a);
register b_reg(clk, rst, temp_b, en_b, b);
register c_reg(clk, rst, temp_c, en_c, c);

alu my_alu(a, b, alu_control, temp_c);

always @(*)
begin
	if (sel_a_path == 1'b0)
		temp_a <= in;
	else
		temp_a <= c;
		
	if (sel_b_path == 1'b0)
		temp_b <= in;
	else
		temp_b <= c;
		
	if (val_to_display == 2'b00)
		seg7_val <= c;
	else if (val_to_display == 2'b01)
		seg7_val <= a;
	else if (val_to_display == 2'b10)
		seg7_val <= b;
	else
		seg7_val <= in;

end
endmodule




module alu(
input [7:0]a,
input [7:0]b,
input [2:0]alu_control,
output reg[7:0]result);

reg [7:0]carry;
reg [7:0]comp_a;
reg [7:0]comp_b;
wire [7:0] dividend;
wire [7:0] divisor;
wire rst;
reg [7:0] quotient;
reg [7:0] remainder;
reg [7:0] temp_dividend;
reg [3:0] shift_count;

always @(*)
begin
	if (alu_control == 3'b000) begin
		if (a[7] == 0 && b[7] == 0) begin
			carry[0] = 0;
			result[0] = a[0] ^ b[0] ^ carry[0];
			carry[1] = (a[0] & b[0]) | (a[0] & carry[0]) | (b[0] & carry[0]);
			result[1] = a[1] ^ b[1] ^ carry[1];
			carry[2] = (a[1] & b[1]) | (a[1] & carry[1]) | (b[1] & carry[1]);
			result[2] = a[2] ^ b[2] ^ carry[2];
			carry[3] = (a[2] & b[2]) | (a[2] & carry[2]) | (b[2] & carry[2]);
			result[3] = a[3] ^ b[3] ^ carry[3];
			carry[4] = (a[3] & b[3]) | (a[3] & carry[3]) | (b[3] & carry[3]);
			result[4] = a[4] ^ b[4] ^ carry[4];
			carry[5] = (a[4] & b[4]) | (a[4] & carry[4]) | (b[4] & carry[4]);
			result[5] = a[5] ^ b[5] ^ carry[5];
			carry[6] = (a[5] & b[5]) | (a[5] & carry[5]) | (b[5] & carry[5]);
			result[6] = a[6] ^ b[6] ^ carry[6];
			carry[7] = (a[6] & b[6]) | (a[6] & carry[6]) | (b[6] & carry[6]);
			result[7] = a[7] ^ b[7] ^ carry[7];
		end else if (a[7] == 1 && b[7] == 1) begin
			comp_a = ~a;
			comp_a = comp_a + 1;
			comp_b = ~b;
			comp_b = comp_b + 1;
			carry[0] = 0;
			result[0] = comp_a[0] ^ comp_b[0] ^ carry[0];
			carry[1] = (comp_a[0] & comp_b[0]) | (comp_a[0] & carry[0]) | (comp_b[0] & carry[0]);
			result[1] = comp_a[1] ^ comp_b[1] ^ carry[1];
			carry[2] = (comp_a[1] & comp_b[1]) | (comp_a[1] & carry[1]) | (comp_b[1] & carry[1]);
			result[2] = comp_a[2] ^ comp_b[2] ^ carry[2];
			carry[3] = (comp_a[2] & comp_b[2]) | (comp_a[2] & carry[2]) | (comp_b[2] & carry[2]);
			result[3] = comp_a[3] ^ comp_b[3] ^ carry[3];
			carry[4] = (comp_a[3] & comp_b[3]) | (comp_a[3] & carry[3]) | (comp_b[3] & carry[3]);
			result[4] = comp_a[4] ^ comp_b[4] ^ carry[4];
			carry[5] = (comp_a[4] & comp_b[4]) | (comp_a[4] & carry[4]) | (comp_b[4] & carry[4]);
			result[5] = comp_a[5] ^ comp_b[5] ^ carry[5];
			carry[6] = (comp_a[5] & comp_b[5]) | (comp_a[5] & carry[5]) | (comp_b[5] & carry[5]);
			result[6] = comp_a[6] ^ comp_b[6] ^ carry[6];
			carry[7] = (comp_a[6] & comp_b[6]) | (comp_a[6] & carry[6]) | (comp_b[6] & carry[6]);
			result[7] = comp_a[7] ^ comp_b[7] ^ carry[7];
			result = result - 1;
			result = ~result;
		end else if (a[7] == 1 && b[7] == 0) begin
			carry[0] = 0;
			result[0] = a[0] ^ b[0] ^ carry[0];
			carry[1] = (a[0] & b[0]) | (a[0] & carry[0]) | (b[0] & carry[0]);
			result[1] = a[1] ^ b[1] ^ carry[1];
			carry[2] = (a[1] & b[1]) | (a[1] & carry[1]) | (b[1] & carry[1]);
			result[2] = a[2] ^ b[2] ^ carry[2];
			carry[3] = (a[2] & b[2]) | (a[2] & carry[2]) | (b[2] & carry[2]);
			result[3] = a[3] ^ b[3] ^ carry[3];
			carry[4] = (a[3] & b[3]) | (a[3] & carry[3]) | (b[3] & carry[3]);
			result[4] = a[4] ^ b[4] ^ carry[4];
			carry[5] = (a[4] & b[4]) | (a[4] & carry[4]) | (b[4] & carry[4]);
			result[5] = a[5] ^ b[5] ^ carry[5];
			carry[6] = (a[5] & b[5]) | (a[5] & carry[5]) | (b[5] & carry[5]);
			result[6] = a[6] ^ b[6] ^ carry[6];
			carry[7] = (a[6] & b[6]) | (a[6] & carry[6]) | (b[6] & carry[6]);
			result[7] = a[7] ^ b[7] ^ carry[7];
		end else if (a[7] == 0 && b[7] == 1) begin
			carry[0] = 0;
			result[0] = a[0] ^ b[0] ^ carry[0];
			carry[1] = (a[0] & b[0]) | (a[0] & carry[0]) | (b[0] & carry[0]);
			result[1] = a[1] ^ b[1] ^ carry[1];
			carry[2] = (a[1] & b[1]) | (a[1] & carry[1]) | (b[1] & carry[1]);
			result[2] = a[2] ^ b[2] ^ carry[2];
			carry[3] = (a[2] & b[2]) | (a[2] & carry[2]) | (b[2] & carry[2]);
			result[3] = a[3] ^ b[3] ^ carry[3];
			carry[4] = (a[3] & b[3]) | (a[3] & carry[3]) | (b[3] & carry[3]);
			result[4] = a[4] ^ b[4] ^ carry[4];
			carry[5] = (a[4] & b[4]) | (a[4] & carry[4]) | (b[4] & carry[4]);
			result[5] = a[5] ^ b[5] ^ carry[5];
			carry[6] = (a[5] & b[5]) | (a[5] & carry[5]) | (b[5] & carry[5]);
			result[6] = a[6] ^ b[6] ^ carry[6];
			carry[7] = (a[6] & b[6]) | (a[6] & carry[6]) | (b[6] & carry[6]);
			result[7] = a[7] ^ b[7] ^ carry[7];
		end	
	end else if (alu_control == 3'b001) begin
		if (a[7] == 0 && b[7] == 0) begin
			comp_b = ~b;
			comp_b = comp_b + 1;
			carry[0] = 0;
			result[0] = a[0] ^ comp_b[0] ^ carry[0];
			carry[1] = (a[0] & comp_b[0]) | (a[0] & carry[0]) | (comp_b[0] & carry[0]);
			result[1] = a[1] ^ comp_b[1] ^ carry[1];
			carry[2] = (a[1] & comp_b[1]) | (a[1] & carry[1]) | (comp_b[1] & carry[1]);
			result[2] = a[2] ^ comp_b[2] ^ carry[2];
			carry[3] = (a[2] & comp_b[2]) | (a[2] & carry[2]) | (comp_b[2] & carry[2]);
			result[3] = a[3] ^ comp_b[3] ^ carry[3];
			carry[4] = (a[3] & comp_b[3]) | (a[3] & carry[3]) | (comp_b[3] & carry[3]);
			result[4] = a[4] ^ comp_b[4] ^ carry[4];
			carry[5] = (a[4] & comp_b[4]) | (a[4] & carry[4]) | (comp_b[4] & carry[4]);
			result[5] = a[5] ^ comp_b[5] ^ carry[5];
			carry[6] = (a[5] & comp_b[5]) | (a[5] & carry[5]) | (comp_b[5] & carry[5]);
			result[6] = a[6] ^ comp_b[6] ^ carry[6];
			carry[7] = (a[6] & comp_b[6]) | (a[6] & carry[6]) | (comp_b[6] & carry[6]);
			result[7] = a[7] ^ comp_b[7] ^ carry[7];
		end if (a[7] == 1 && b[7] == 1) begin
			comp_b = ~b;
			comp_b = comp_b + 1;
			carry[0] = 0;
			result[0] = a[0] ^ comp_b[0] ^ carry[0];
			carry[1] = (a[0] & comp_b[0]) | (a[0] & carry[0]) | (comp_b[0] & carry[0]);
			result[1] = a[1] ^ comp_b[1] ^ carry[1];
			carry[2] = (a[1] & comp_b[1]) | (a[1] & carry[1]) | (comp_b[1] & carry[1]);
			result[2] = a[2] ^ comp_b[2] ^ carry[2];
			carry[3] = (a[2] & comp_b[2]) | (a[2] & carry[2]) | (comp_b[2] & carry[2]);
			result[3] = a[3] ^ comp_b[3] ^ carry[3];
			carry[4] = (a[3] & comp_b[3]) | (a[3] & carry[3]) | (comp_b[3] & carry[3]);
			result[4] = a[4] ^ comp_b[4] ^ carry[4];
			carry[5] = (a[4] & comp_b[4]) | (a[4] & carry[4]) | (comp_b[4] & carry[4]);
			result[5] = a[5] ^ comp_b[5] ^ carry[5];
			carry[6] = (a[5] & comp_b[5]) | (a[5] & carry[5]) | (comp_b[5] & carry[5]);
			result[6] = a[6] ^ comp_b[6] ^ carry[6];
			carry[7] = (a[6] & comp_b[6]) | (a[6] & carry[6]) | (comp_b[6] & carry[6]);
			result[7] = a[7] ^ comp_b[7] ^ carry[7];
		end if (a[7] == 1 && b[7] == 0) begin
			comp_b = ~b;
			comp_b = comp_b + 1;
			carry[0] = 0;
			result[0] = a[0] ^ comp_b[0] ^ carry[0];
			carry[1] = (a[0] & comp_b[0]) | (a[0] & carry[0]) | (comp_b[0] & carry[0]);
			result[1] = a[1] ^ comp_b[1] ^ carry[1];
			carry[2] = (a[1] & comp_b[1]) | (a[1] & carry[1]) | (comp_b[1] & carry[1]);
			result[2] = a[2] ^ comp_b[2] ^ carry[2];
			carry[3] = (a[2] & comp_b[2]) | (a[2] & carry[2]) | (comp_b[2] & carry[2]);
			result[3] = a[3] ^ comp_b[3] ^ carry[3];
			carry[4] = (a[3] & comp_b[3]) | (a[3] & carry[3]) | (comp_b[3] & carry[3]);
			result[4] = a[4] ^ comp_b[4] ^ carry[4];
			carry[5] = (a[4] & comp_b[4]) | (a[4] & carry[4]) | (comp_b[4] & carry[4]);
			result[5] = a[5] ^ comp_b[5] ^ carry[5];
			carry[6] = (a[5] & comp_b[5]) | (a[5] & carry[5]) | (comp_b[5] & carry[5]);
			result[6] = a[6] ^ comp_b[6] ^ carry[6];
			carry[7] = (a[6] & comp_b[6]) | (a[6] & carry[6]) | (comp_b[6] & carry[6]);
			result[7] = a[7] ^ comp_b[7] ^ carry[7];
		end if (a[7] == 0 && b[7] == 1) begin
			comp_b = ~b;
			comp_b = comp_b + 1;
			carry[0] = 0;
			result[0] = a[0] ^ comp_b[0] ^ carry[0];
			carry[1] = (a[0] & comp_b[0]) | (a[0] & carry[0]) | (comp_b[0] & carry[0]);
			result[1] = a[1] ^ comp_b[1] ^ carry[1];
			carry[2] = (a[1] & comp_b[1]) | (a[1] & carry[1]) | (comp_b[1] & carry[1]);
			result[2] = a[2] ^ comp_b[2] ^ carry[2];
			carry[3] = (a[2] & comp_b[2]) | (a[2] & carry[2]) | (comp_b[2] & carry[2]);
			result[3] = a[3] ^ comp_b[3] ^ carry[3];
			carry[4] = (a[3] & comp_b[3]) | (a[3] & carry[3]) | (comp_b[3] & carry[3]);
			result[4] = a[4] ^ comp_b[4] ^ carry[4];
			carry[5] = (a[4] & comp_b[4]) | (a[4] & carry[4]) | (comp_b[4] & carry[4]);
			result[5] = a[5] ^ comp_b[5] ^ carry[5];
			carry[6] = (a[5] & comp_b[5]) | (a[5] & carry[5]) | (comp_b[5] & carry[5]);
			result[6] = a[6] ^ comp_b[6] ^ carry[6];
			carry[7] = (a[6] & comp_b[6]) | (a[6] & carry[6]) | (comp_b[6] & carry[6]);
			result[7] = a[7] ^ comp_b[7] ^ carry[7];
		end
	end else if (alu_control == 3'b010) begin
		result[0] = b[0] * a[0];
		result[1] = b[0] * a[1];
		result[2] = (b[0] * a[2]) + (b[1] * a[0]);
		result[3] = (b[0] * a[3]) + (b[1] * a[1] )+ (b[2] * a[0]);
		result[4] = (b[1] * a[2]) + (b[2] * a[1] )+ (b[3] * a[0]);
		result[5] = (b[1] * a[3]) + (b[2] * a[2] )+ (b[3] * a[1]);
		result[6] = (b[2] * a[3]) + (b[2] * a[3]);
		result[7] = (b[3] * a[3]);
	end else if (alu_control == 3'b011) begin
  			if (rst == 1'b0) begin
    				quotient <= 8'b0;
    				remainder <= 8'b0;
    				temp_dividend <= 8'b0;
    				shift_count <= 4'b0;
  			end else begin
    				if (temp_dividend >= divisor) begin
      					temp_dividend <= temp_dividend - divisor;
      					quotient[7] <= 1;
    				end else begin
      					temp_dividend <= temp_dividend << 1;
     					quotient[7] <= 0;
    				end
    				quotient[6:0] <= quotient[7:1];
    				shift_count <= shift_count + 1;
    				if (shift_count == 8) begin
      					remainder <= temp_dividend;
    				end
		end
	end else if (alu_control == 3'b100) begin
		if (b == 0) begin
  			result = 1;
		end else begin 
		if (b > 0 & b % 2 == 0) begin
   			result = (a^(b/2))^2;
		end else begin
		    if (b > 0 & b % 2 == 1)
   			result = (a^((b-1)/2))^2 * a;
	   end
	end
end
end
endmodule



module register(
input clk, 
input rst, 
input [7:0]in, 
input en, 
output reg [7:0]out);

always @(posedge clk or negedge rst)
begin
	if (rst == 1'b0)
		out <= 8'b00000000;
	else if (en == 1'b1)
		out <= in;
end

endmodule



module three_decimal_vals_w_neg (
input [7:0]val,
output [6:0]seg7_neg_sign,
output [6:0]seg7_dig0,
output [6:0]seg7_dig1,
output [6:0]seg7_dig2
);

reg [3:0] result_one_digit;
reg [3:0] result_ten_digit;
reg [3:0] result_hun_digit;
reg result_is_negative;
reg [7:0]twos_comp;

always @(*)
begin
	result_is_negative = val[7];
	if (result_is_negative == 1) begin
		twos_comp = ~val;
		twos_comp = twos_comp + 1;
	end else
		twos_comp = val;
	
	if (twos_comp >= 7'b1100100) begin
		result_hun_digit = twos_comp / 100;
		result_ten_digit = twos_comp / 10 % 10;
		result_one_digit = twos_comp % 100;
	end else begin
		result_hun_digit = 1'b0;
		result_ten_digit = twos_comp / 10;
		result_one_digit = twos_comp % 10;
	end
	 
end

seven_segment one (result_one_digit, seg7_dig0);
seven_segment ten (result_ten_digit, seg7_dig1);
seven_segment hun (result_hun_digit, seg7_dig2);
seven_segment_negative neg (result_is_negative, seg7_neg_sign);

endmodule



module seven_segment (
input [3:0]i,
output reg [6:0]o
);

always @(*)
begin
	case (i)	   
		4'b0000: o = 7'b1000000;
		4'b0001: o = 7'b1111001;
		4'b0010: o = 7'b0100100;
		4'b0011: o = 7'b0110000;
		4'b0100: o = 7'b0011001;
		4'b0101: o = 7'b0010010;
		4'b0110: o = 7'b0000010;
		4'b0111: o = 7'b1111000;
		4'b1000: o = 7'b0000000;
		4'b1001: o = 7'b0010000;
		4'b1010: o = 7'b0001000;
		4'b1011: o = 7'b0000011;
		4'b1100: o = 7'b1000110;
		4'b1101: o = 7'b0100001;
		4'b1110: o = 7'b0000110;
		4'b1111: o = 7'b0001110;
		default: o = 7'b1111111;
	endcase
end

endmodule



module seven_segment_negative(i,o);

input i;
output reg [6:0]o; 

always @(*)
begin
	case (i)	    
		1'b1: o = 7'b0111111;
		default: o = 7'b1111111;
	endcase		
end

endmodule
