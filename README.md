# Algoritmo-de-contagem-de-passageiros
Olá a todos que chegaram até aqui para ver nosso trabalho, hoje apresentamos nosso primeiro projeto como alunos do SENAI da turma de 2025.

O desafio que nos foi dado foi criar um algoritmo que recebe uma lista de linhas de ônibus e várias viagens feitas sobre essas linhas com os valores de pessoas que embarcaram e desembarcaram em cada ponto de parada.

ARQUIVO WORD:
[Arquivo LeiaMe.docx](https://github.com/user-attachments/files/21927251/Arquivo.LeiaMe.docx)

FLUXOGRAMA:
<img width="3240" height="2137" alt="Cópia de fluxograma do sistema de passageiros" src="https://github.com/user-attachments/assets/ee81b0c8-03bf-4072-9ca4-6fd7545d71a9" />



algoritmo:
[main (1).py](https://github.com/user-attachments/files/21927260/main.1.py)
    
from collections import defaultdict

arquivo = r'C:\Users\joao_oliveira171\Documents\out.csv'
grupos = defaultdict(lambda: {'total': 0})


with open(arquivo, encoding='utf-8') as f:
    for idx_arquivo, linha in enumerate(f, start=1):
        if not linha.strip():
            continue
        partes = linha.strip().split(',')
        grupo = int(partes[0])
        soma = sum(int(p.split(':')[1]) for p in partes[1:] if ':' in p and p.split(':')[1])

      g = grupos[grupo]
      g['total'] += soma
        
print("RANKING DE ÔNIBUS:")
print("============================")
for posicao, (grupo, dados) in enumerate(
        sorted(grupos.items(), key=lambda item: item[1]["total"], reverse=True), start=1):
    print(f"{posicao}º lugar - ônibus {grupo}: atende {dados['total']} passageiros")

mais_passageiros = max(grupos.items(), key=lambda item: item[1]["total"])
menos_passageiros = min(grupos.items(), key=lambda item: item[1]["total"])

print("\nDESTAQUES:")
print("==========")
print(f" Maior número de passageiros: ônibus {mais_passageiros[0]} com {mais_passageiros[1]['total']} passageiros")
print(f"Menor número de passageiros:  ônibus {menos_passageiros[0]} com {menos_passageiros[1]['total']} passageiros")
