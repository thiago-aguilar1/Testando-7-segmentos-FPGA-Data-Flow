# Testando-7-segmentos-FPGA-Data-Flow
Programa para testar o funcionamento do display 7 segmento, conforme a entrada.

```verilog

module testandoDisplay (
						input [1:0] a,   // tem 2 bits
						output a1, b1, c1, d1, e1, f1, g1, a2, b2, c2, d2, e2, f2, g2
						);
wire [6:0] seteSegmentos1;		
wire [6:0] seteSegmentos2;				
wire [2:0] constante;     // tem 3 bits, para que não se perda o bit msb na multiplicação
wire [2:0] entrada;   //que vai armazenar o valor a em um espaço maior
wire [2:0] produto; 

assign constante = 3'b010;
assign entrada = { 1'b0, a};
assign produto =  entrada * constante;

assign seteSegmentos1 = (a == 2'b00) ? 7'b1111110 :
					   (a == 2'b01) ? 7'b0110000 :
					   (a == 2'b10) ? 7'b1101101 : 7'b1111001;

assign {a1, b1, c1, d1, e1, f1, g1} = seteSegmentos1;

assign seteSegmentos2 = (produto == 3'b000) ? 7'b1111110 :
					   (produto == 3'b010) ? 7'b1101101 :
					   (produto == 3'b100) ? 7'b0110011 : 7'b1011111;
					   
assign {a2, b2, c2, d2, e2, f2, g2} = seteSegmentos2;

endmodule
			



```


![Forma de onda](https://github.com/thiago-aguilar1/Testando-7-segmentos-FPGA-Data-Flow/blob/main/image.png)


## Observação:

 * Projeto teste para um [projeto maior](https://github.com/thiago-aguilar1/Mutiplier-and-Display-7-FPGA-Dataflow-Modeling), em que nos foi imposto a tarefa de implementar um multiplicador que apresente o valor de entrada e o valor do produto em displays de 7 segmentos, com o desafio de usar **apenas** a modelagem por fluxo de dados (Data Flow Modeling).
 * Neste projeto teste,  uma entrada de 2 bits é multiplicada por 2. O valor da entrada é apresentada em um display de 7 segmentos, e o valor do produto é apresentado em outro display de 7 segmentos.




