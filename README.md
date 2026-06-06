Sistema de cálculo (calculadora) para açougue. 
****

1. Seleção da Peça Base (Rendimento Relativo)
Cada tipo de peça cadastrada (Bovino Inteiro, Dianteiro, Traseiro, Banda Direita e Banda Esquerda) possui uma tabela exclusiva de proporções de corte. Essas proporções são baseadas em dados técnicos reais de rendimento de carcaça:
Boi Inteiro (Carcaça Completa): Apresenta uma quebra de 20% em média devido a ossos grandes, sebo e perda por desidratação (quebra fria). Os outros 80% são distribuídos proporcionalmente entre os 23 cortes de carne.
Dianteiro Bovino: Possui a maior proporção de perda em osso (escapular e costelas de agulha), totalizando cerca de 30% de descarte (osso e gordura) e 70% de carne limpa aproveitável (acém, peito, paleta).
Traseiro Bovino: Região mais nobre que apresenta apenas 15% de quebra esquelética e gordura excedente, gerando 85% de carne limpa comercializável (picanha, alcatra, filé, coxão mole).

2. Lógica Matemática de Divisão do Peso
Quando o operador lança o Peso Bruto de Entrada ($P_{bruto}$) na calculadora, o sistema lê a tabela da peça selecionada e aplica a seguinte fórmula para cada um dos 23 cortes cadastrados:
$$\text{Peso Estimado do Corte} = \frac{P_{bruto} \times \text{Percentual do Corte (\%)}}{100}$$
Exemplo Prático (Se você lançar 10 kg de Boi Inteiro):
Picanha (1,5%): $\frac{10 \times 1,5}{100} = 0,15\text{ kg}$ de Picanha limpa.
Coxão Mole (10%): $\frac{10 \times 10}{100} = 1,00\text{ kg}$ de Coxão Mole.
Ossos e Quebra (20% - Desperdício): $\frac{10 \times 20}{100} = 2,00\text{ kg}$ de perda.
Soma Total: A soma de todos os cortes calculados será rigorosamente igual aos 10 kg de entrada, assegurando que não haja fuga ou ganho fantasma de peso.

3. Separação de Carne Limpa e Perdas (Desperdício)
Cada item na tabela possui um atributo lógico booleano chamado desperdicio (verdadeiro/falso):
Se desperdicio: true (ossos e sebo), o peso calculado daquele item é adicionado ao acumulador de Desperdício/Quebra.
Se desperdicio: false (carnes de primeira, nobres ou de segunda), o peso calculado daquele item é somado ao acumulador de Carne Limpa Aproveitada.
Isso impede que o sistema calcule um rendimento falso de 100% de carne, refletindo a perda óssea real que o açougueiro tem no balcão.

4. Formulação Financeira e Sistema de Vendas
O faturamento estimado é calculado multiplicando o peso de cada carne aproveitável pelo seu valor de mercado:
$$\text{Valor Comercial do Corte} = \text{Peso Estimado do Corte (kg)} \times \text{Preço de Venda do Corte (R\$/kg)}$$
O sistema soma os valores comerciais de todos os cortes para chegar ao Faturamento Bruto Estimado daquela carcaça, fornecendo a base exata para o estoque e o preço de venda que o cliente usará no sistema de vendas (PDV).

