# USE-OF-TIMERS-IN-TRAFFIC-LIGHT-CONTROLLER-
Traffic congestion is a growing problem in urban areas, leading to delays, pollution, and safety  concerns. Traffic light controllers equipped with timers are fundamental in mitigating these issues  by regulating the flow of vehicles and pedestrians. Timers manage the duration of signal phases.:
Verilog code :

`timescale 1ns / 1ps

module traffic_light_controller(

 output reg [2:0] n_lights, // North lights

 output reg [2:0] s_lights, // South lights

 output reg [2:0] e_lights, // East lights

 output reg [2:0] w_lights, // West lights

 input clk, // Clock signal

 input rst_n // Reset signal (active low)

);

 parameter [2:0] north_green = 3'b001; // North green

 parameter [2:0] north_yellow = 3'b010; // North yellow

 parameter [2:0] south_green = 3'b100; // South green

 parameter [2:0] south_yellow = 3'b101; // South yellow

 parameter [2:0] east_green = 3'b110; // East green

 parameter [2:0] east_yellow = 3'b111; // East yellow

 parameter [2:0] west_green = 3'b000; // West green

 parameter [2:0] west_yellow = 3'b011; // West yellow
 reg [2:0] state; // Current state

 reg [3:0] timer; // Timer for light duration

 always @(posedge clk or negedge rst_n) begin

 if (!rst_n) begin

 state <= north_green; // Start with north green

 timer <= 0; // Reset timer

 end else begin

 case (state)

 north_green: begin

 n_lights <= north_green;

 s_lights <= 3'b100; // South red

 e_lights <= 3'b100; // East red

 w_lights <= 3'b100; // West red

 if (timer == 4'd8) begin // Green for 8 clock cycles

 state <= north_yellow;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 north_yellow: begin

 n_lights <= north_yellow;

 s_lights <= 3'b100; // South red

 e_lights <= 3'b100; // East red

 w_lights <= 3'b100; // West red

 if (timer == 4'd4) begin // Yellow for 4 clock cycles

 state <= south_green;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 endend

 south_green: begin

 n_lights <= 3'b100; // North red

 s_lights <= south_green;

 e_lights <= 3'b100; // East red

 w_lights <= 3'b100; // West red

 if (timer == 4'd8) begin // Green for 8 clock cycles

 state <= south_yellow;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 south_yellow: begin

 n_lights <= 3'b100; // North red

 s_lights <= south_yellow;

 e_lights <= 3'b100; // East red

 w_lights <= 3'b100; // West red

 if (timer == 4'd4) begin // Yellow for 4 clock cycles

 state <= east_green;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 east_green: begin

 n_lights <= 3'b100; // North red

 s_lights <= 3'b100; // South red

 e_lights <= east_green;w_lights <= 3'b100; // West red

 if (timer == 4'd8) begin // Green for 8 clock cycles

 state <= east_yellow;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 east_yellow: begin

 n_lights <= 3'b100; // North red

 s_lights <= 3'b100; // South red

 e_lights <= east_yellow;

 w_lights <= 3'b100; // West red

 if (timer == 4'd4) begin // Yellow for 4 clock cycles

 state <= west_green;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 

 west_green: begin

 n_lights <= 3'b100; // North red

 s_lights <= 3'b100; // South red

 e_lights <= 3'b100;

 w_lights <= west_green; 

 if (timer == 4'd8) begin // Green for 8 clock cycles

 state <= west_yellow;

 timer <= 0;

 end else begin

 timer <= timer + 1;end

 end

 east_yellow: begin

 n_lights <= 3'b100; // North red

 s_lights <= 3'b100; // South red

 e_lights <= 

 w_lights <= 3'b100; // West red

 if (timer == 4'd4) begin // Yellow for 4 clock cycles

 state <= north_green;

 timer <= 0;

 end else begin

 timer <= timer + 1;

 end

 end

 endcase

 end

 end

endmodule
