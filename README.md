 Automação Protheus - Baixa de Títulos (RPA)

O problema que sempre acontece é que, na hora de realizar as baixas via retorno CNAB, alguns títulos apresentam erro e não são baixados, tendo que ser feitos de maneira manual. Como o volume diário é alto, baixar um por um manualmente ocupava um tempo do usuário, que poderia estar fazendo outra coisa. Então, o código pega os números do boleto do banco e realiza a baixa

Este projeto é um script de automação (RPA) desenvolvido em Python utilizando a biblioteca Playwright. O objetivo é automatizar o processo repetitivo de baixa de títulos no módulo Financeiro (Contas a Receber) do ERP TOTVS Protheus Web. 

O robô realiza login, navega até a rotina, aplica filtros de forma resiliente, preenche os dados da baixa e gera um relatório final de execução.

 Funcionalidades
Login Automático: Acesso seguro ao ambiente Protheus Web.

Troca de Contexto: Seleção automática de Módulo e alteração da Data Base do sistema.

Filtros Inteligentes: Lógica de retry (tentativa) caso o menu de filtros falhe ao abrir, garantindo estabilidade.

Tratamento de Loader: O script aguarda os carregamentos internos do Protheus (spinners/loaders) para evitar cliques em falso.

Seleção de Motivo: Navegação automatizada nos comboboxes de motivo da baixa.

Relatório Final: Exibe no terminal um resumo detalhado dos títulos baixados com sucesso e dos erros encontrados.

 Tecnologias Utilizadas
Python 3.x

Playwright (Automação de Browser)

python-dotenv (Gestão de variáveis de ambiente)


Insira os números dos boletos que deseja baixar na variável raw_titulos:

Python
raw_titulos = """
000000046193
000000046367
...
"""
Verifique se a data base definida no código (14/01/2026) está correta para o seu lote.

Execute o script:

Bash
python main.py
Lógica de Segurança
O script possui travas de segurança e tratamentos de exceção:

Modo Produção: O script atual está configurado para salvar as alterações.

Tratamento de Erros: Caso ocorra erro em um título específico, o robô fecha as janelas de erro, registra a falha no relatório e pula para o próximo título, sem interromper todo o lote.

Exemplo de Saída (Relatório)
Ao final da execução, o console exibirá:

Plaintext
############################################################
RELATÓRIO FINAL DE EXECUÇÃO
############################################################
Total: 23 | Sucessos: 22 | Falhas: 1
------------------------------------------------------------

✅ SUCESSOS:
   -> 000000046193
   -> 000000046367
   ...

❌ ERROS:
   -> 000000050820 | Erro: Element not found...
############################################################

📝 Autor
Sergio Lopes
