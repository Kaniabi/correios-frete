# correios-frete [<img src="https://secure.travis-ci.org/adonescunha/correios-frete.png?branch=master">](http://travis-ci.org/adonescunha/correios-frete)

Cliente Python para o [WebService dos Correios](http://www.correios.com.br/webservices/), para calcular os preços e prazos de entregas de encomendas.

## Uso

Crie um pacote:

```python
from correios_frete import *
from correios_frete.constants import CAIXA_PACOTE

package = Package(formato=CAIXA_PACOTE)
```

Adicione itens ao pacote:

```python
package.add_item(
    weight = 0.5,
    height = 6.0,
    width  = 16.0,
    length = 16.0
)
```

Inicialize o cliente do WebService:

```python
client = Client(cep_origem='01310-200')
```

Chame o método do WebService desejado:

```python
from correios_frete.constants import SEDEX, PAC

servicos = client.calc_preco_prazo(package, '52020-010', SEDEX, PAC)
servicos[0].codigo        # 40010 (SEDEX)
servicos[0].valor         # 56.8
servicos[0].prazo_entrega # 1
servicos[1].codigo        # 41106 (PAC)
servicos[1].valor         # 21.9
servicos[1].prazo_entrega # 9
```

## Informações adicionais

### Parâmetros do cliente do WebService

```python
cep_origem        # CEP de Origem sem hífen.Exemplo: 05311900
codigo_empresa    # Seu código administrativo junto à ECT
senha             # Senha para acesso ao serviço, associada ao seu código administrativo
valor_declarado   # Indica se a encomenda será entregue com o serviço adicional valor declarado.
aviso_recebimento # Indica se a encomenda será entregue com o serviço  adicional aviso de recebimento
```

### Formatos do pacote

```python
CAIXA_PACOTE = 1 # Formato caixa/pacote
ROLO_PRISMA  = 2 # Formato rolo/prisma
ENVELOPE     = 3 # Envelope
```

### Serviços suportados

```python
SEDEX                       = '40010'               # SEDEX sem contrato
SEDEX_A_COBRAR              = '40045'               # SEDEX a cobrar, sem contrato
SEDEX_A_COBRAR_COM_CONTRATO = '40126'               # SEDEX a cobrar, com contrato
SEDEX_10                    = '40215'               # SEDEX 10, sem contrato
SEDEX_HOJE                  = '40290'               # SEDEX Hoje, sem contrato
SEDEX_COM_CONTRATO_1        = '40096'               # SEDEX com contrato
SEDEX_COM_CONTRATO_2        = '40436'               # SEDEX com contrato
SEDEX_COM_CONTRATO_3        = '40444'               # SEDEX com contrato
SEDEX_COM_CONTRATO_4        = '40568'               # SEDEX com contrato
SEDEX_COM_CONTRATO_5        = '40606'               # SEDEX com contrato
SEDEX_COM_CONTRATO          = SEDEX_COM_CONTRATO_1  # SEDEX com contrato
PAC                         = '41106'               # PAC, sem contrato
PAC_COM_CONTRATO            = '41068'               # PAC, com contrato
E_SEDEX                     = '81019'               # e-SEDEX, com contrato
E_SEDEX_PRIORITARIO         = '81027'               # e-SEDEX prioritário, com contrato
E_SEDEX_EXPRESS             = '81035'               # e-SEDEX Express, com contrato
GRUPO_1_E_SEDEX             = '81868'               # (Grupo 1) e-SEDEX, com contrato
GRUPO_2_E_SEDEX             = '81833'               # (Grupo 2) e-SEDEX, com contrato
GRUPO_3_E_SEDEX             = '81850'               # (Grupo 3) e-SEDEX, com contrato
```

### Métodos do WebService

```python
client.calc_preco_data       # CalcPrecoData
client.calc_preco_prazo      # CalcPrecoPrazo
client.calc_prazo            # CalcPrazo
client.calc_preco            # CalcPreco
client.calc_prezo_prazo_data # CalcPrezoPrazoData
client.calc_prazo_data       # CalcPrecoData
```
