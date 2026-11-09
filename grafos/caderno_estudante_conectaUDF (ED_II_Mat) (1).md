RESOLUÇÂO NO FINAL DO DOCUMENTO

# Caderno do Estudante
# Projeto ConectaUDF: redes sociais com grafos
**Disciplina:** Algoritmos / Matemática Discreta / Ciência de Dados

## 1. O desafio
Você faz parte da equipe que analisa a rede social fictícia **ConectaUDF**. Sua missão é representar as amizades em um grafo, realizar cálculos e usar Python para interpretar a estrutura da rede.

## 2. Conceitos essenciais
- **Vértice (ou nó):** representa um usuário.
- **Aresta:** representa uma amizade entre dois usuários.
- **Grau:** quantidade de conexões diretas de um usuário.
- **Caminho:** sequência de usuários em que cada par consecutivo está conectado.
- **Densidade:** proporção entre as amizades existentes e todas as amizades possíveis.

Neste projeto, a amizade é recíproca. Portanto, usamos um **grafo não direcionado**.

## 3. Conheça os usuários
| Código | Usuário |
|---|---|
| A | Ana |
| B | Bruno |
| C | Carla |
| D | Diego |
| E | Elisa |
| F | Felipe |

As amizades são:
1. Ana — Bruno
2. Ana — Carla
3. Bruno — Carla
4. Bruno — Diego
5. Carla — Elisa
6. Diego — Elisa
7. Diego — Felipe
8. Elisa — Felipe

## 4. Passo a passo: desenhe o grafo
1. Desenhe seis círculos, um para cada usuário.
2. Escreva o nome de cada pessoa dentro do círculo.
3. Para cada amizade da lista, desenhe uma linha entre os dois usuários.
4. Não desenhe duas linhas para a mesma amizade.
5. Confira se todas as oito amizades aparecem.

**Espaço para o seu desenho:** faça o grafo no caderno ou em uma ferramenta de desenho.

## 5. Passo a passo: calcule o grau
Conte quantas linhas chegam a cada círculo. Registre o resultado.

| Usuário | Amigos diretos | Grau |
|---|---|---:|
| Ana | __________________ | ____ |
| Bruno | __________________ | ____ |
| Carla | __________________ | ____ |
| Diego | __________________ | ____ |
| Elisa | __________________ | ____ |
| Felipe | __________________ | ____ |

**Pergunta 1:** quem tem mais conexões diretas?  
Resposta: __________________________________________________

## 6. Passo a passo: calcule o número de amizades
Some todos os graus. Como cada amizade conecta dois usuários, cada aresta é contada duas vezes.

**Fórmula:**  
`Número de arestas = soma dos graus ÷ 2`

1. Soma dos graus: ______
2. Divida por 2: ______ ÷ 2 = ______
3. Quantas amizades existem no grafo? ______

## 7. Passo a passo: calcule a densidade
A densidade compara as amizades existentes com o total de amizades possíveis.

Para um grafo simples não direcionado:

`D = 2 × E / (V × (V − 1))`

Em que:
- `D` = densidade;
- `E` = número de arestas;
- `V` = número de vértices.

Substitua os valores:
`D = 2 × ____ / (____ × (____ − 1))`

Resultado decimal: __________  
Resultado percentual: __________ %

**Interprete:** a rede tem poucas ou muitas das conexões possíveis? Explique com suas palavras.

________________________________________________________________

## 8. Passo a passo: represente o grafo em Python
A lista de adjacência registra, para cada usuário, os nomes de seus amigos. Digite o código em Python (por exemplo, no Google Colab ou em outro ambiente disponível).

```python
rede = {
    "Ana": ["Bruno", "Carla"],
    "Bruno": ["Ana", "Carla", "Diego"],
    "Carla": ["Ana", "Bruno", "Elisa"],
    "Diego": ["Bruno", "Elisa", "Felipe"],
    "Elisa": ["Carla", "Diego", "Felipe"],
    "Felipe": ["Diego", "Elisa"]
}

# Quantidade de usuarios
n = len(rede)

# Calcule o grau de cada usuario
for usuario, amigos in rede.items():
    print(usuario, "tem", len(amigos), "conexoes")

# A soma dos graus conta cada amizade duas vezes
soma_graus = sum(len(amigos) for amigos in rede.values())
arestas = soma_graus // 2

print("Total de usuarios:", n)
print("Total de amizades:", arestas)

# Densidade do grafo
densidade = (2 * arestas) / (n * (n - 1))
print(f"Densidade: {densidade:.2%}")
```

### Entenda o código
1. `rede` guarda os usuários e suas listas de amigos.
2. `len(rede)` conta os usuários.
3. `len(amigos)` calcula o grau de cada usuário.
4. `sum(...)` soma os graus.
5. `// 2` divide a soma por dois para contar cada amizade uma única vez.
6. A fórmula final calcula a densidade.

## 9. Passo a passo: encontre um caminho
Encontre um caminho de Ana até Felipe. Cada passagem por uma linha corresponde a uma aresta.

Exemplo de registro:
`Ana → __________ → __________ → Felipe`

- Quantas arestas há no caminho? ______
- Você encontrou outro caminho com a mesma quantidade de arestas? Qual?

________________________________________________________________

## 10. Desafio em grupo
Amplie a rede social:
1. Adicione pelo menos quatro usuários fictícios.
2. Crie no mínimo cinco novas amizades.
3. Atualize a lista de adjacência no Python.
4. Recalcule os graus, o total de arestas e a densidade.
5. Compare a densidade antes e depois da ampliação.
6. Identifique os usuários com mais conexões.
7. Explique como a rede poderia recomendar uma nova amizade.

## 11. Entrega
Entregue:
- desenho do grafo;
- tabela com os graus;
- cálculos de arestas e densidade;
- código Python executável;
- respostas às perguntas e breve conclusão.

## 12. Pergunta de reflexão
Duas pessoas ainda não são amigas, mas têm três amigos em comum. Como essa informação poderia ser usada para sugerir uma nova conexão? Quais cuidados de privacidade devem ser considerados ao analisar redes sociais?

## Resolucão do desafio
<img width="1350" height="825" alt="grafo_original" src="https://github.com/user-attachments/assets/2193288b-8749-404d-8e14-892668c544ca" />
<img width="1350" height="825" alt="grafo_ampliado (1)" src="https://github.com/user-attachments/assets/e7d2fb75-c38e-4cf9-9901-61c644cf5b76" />


```Python
from collections import deque
from itertools import combinations

# ---------- Rede original ----------
rede = {
    "Kauã": ["Bruno", "Carla"],
    "Bruno": ["Kauã", "Carla", "Diego"],
    "Carla": ["Kauã", "Bruno", "Elisa"],
    "Diego": ["Bruno", "Elisa", "Felipe"],
    "Elisa": ["Carla", "Diego", "Felipe"],
    "Felipe": ["Diego", "Elisa"],
}


def analisar(grafo, titulo):
    print("=" * 50)
    print(titulo)
    print("=" * 50)

    n = len(grafo)
    for usuario, amigos in grafo.items():
        print(usuario, "tem", len(amigos), "conexoes")

    soma_graus = sum(len(amigos) for amigos in grafo.values())
    arestas = soma_graus // 2
    densidade = (2 * arestas) / (n * (n - 1))

    print("Soma dos graus:", soma_graus)
    print("Total de usuarios:", n)
    print("Total de amizades:", arestas)
    print(f"Densidade: {densidade:.2%}")

    maior = max(len(a) for a in grafo.values())
    populares = [u for u, a in grafo.items() if len(a) == maior]
    print("Mais conexoes (grau", maior, "):", ", ".join(populares))
    return arestas, densidade


def todos_caminhos_minimos(grafo, origem, destino):
    """Busca em largura que devolve todos os caminhos de menor tamanho."""
    fila = deque([[origem]])
    melhores = []
    menor = None
    while fila:
        caminho = fila.popleft()
        if menor is not None and len(caminho) > menor:
            break
        atual = caminho[-1]
        if atual == destino:
            menor = len(caminho)
            melhores.append(caminho)
            continue
        for vizinho in grafo[atual]:
            if vizinho not in caminho:
                fila.append(caminho + [vizinho])
    return melhores


def recomendar(grafo, minimo=2):
    """Sugere amizades entre quem ainda nao e amigo, ordenando por amigos em comum."""
    sugestoes = []
    for a, b in combinations(grafo, 2):
        if b not in grafo[a]:
            comuns = sorted(set(grafo[a]) & set(grafo[b]))
            if len(comuns) >= minimo:
                sugestoes.append((len(comuns), a, b, comuns))
    return sorted(sugestoes, reverse=True)


arestas1, dens1 = analisar(rede, "REDE ORIGINAL")

print()
print("Caminhos minimos de Kauã ate Felipe:")
for c in todos_caminhos_minimos(rede, "Kauã", "Felipe"):
    print(" -> ".join(c), "| arestas:", len(c) - 1)

# ---------- Rede ampliada (desafio em grupo) ----------
def adicionar_amizade(grafo, a, b):
    grafo.setdefault(a, [])
    grafo.setdefault(b, [])
    if b not in grafo[a]:
        grafo[a].append(b)
        grafo[b].append(a)


rede2 = {u: list(a) for u, a in rede.items()}
for novo in ["Gabriel", "Helena", "Igor", "Julia"]:
    rede2[novo] = []

novas = [
    ("Felipe", "Gabriel"),
    ("Gabriel", "Helena"),
    ("Helena", "Igor"),
    ("Igor", "Julia"),
    ("Julia", "Kauã"),
    ("Carla", "Helena"),
    ("Diego", "Igor"),
]
for a, b in novas:
    adicionar_amizade(rede2, a, b)

print()
arestas2, dens2 = analisar(rede2, "REDE AMPLIADA")

print()
print(f"Densidade antes: {dens1:.2%} | depois: {dens2:.2%}")

print()
print("Sugestoes de amizade (>= 2 amigos em comum):")
for qtd, a, b, comuns in recomendar(rede2):
    print(f"{a} e {b}: {qtd} em comum ({', '.join(comuns)})")
```

1. Grafo original 

Grafo original

As 8 amizades aparecem uma única vez: 
Kauã—Bruno, 
Kauã—Carla, 
Bruno—Carla, 
Bruno—Diego, 
Carla—Elisa, 
Diego—Elisa, 
Diego—Felipe, 
Elisa—Felipe.

2. Graus 
Usuário	Amigos diretos	Grau
Kauã	Bruno, Carla	2

Bruno	Kauã, Carla, Diego	3

Carla	Kauã, Bruno, Elisa	3

Diego	Bruno, Elisa, Felipe	3

Elisa	Carla, Diego, Felipe	3

Felipe	Diego, Elisa	2


Pergunta 1: quem tem mais conexões diretas? Bruno, Carla, Diego e Elisa empatam, cada um com 3 conexões.

3. Número de amizades 
Soma dos graus: 2 + 3 + 3 + 3 + 3 + 2 = 16
16 ÷ 2 = 8
Existem 8 amizades no grafo.
4. Densidade

D = 2 × 8 / (6 × (6 − 1)) = 16 / 30

Resultado decimal: 0,533

Resultado percentual: 53,3 %

6. Caminho de Kauã até Felipe
 
Kauã → Bruno → Diego → Felipe (3 arestas)

Kauã → Carla → Elisa → Felipe (3 arestas)


Quantas arestas há no caminho? 3

Há outro caminho com a mesma quantidade de arestas? Sim: Kauã → Carla → Elisa → Felipe. Uma busca em largura confirmou que esses são os dois únicos caminhos mínimos; não existe caminho com menos de 3 arestas.

7Novos usuários e amizades

Usuários adicionados: Gabriel, Helena, Igor e Julia (4 usuários).

Novas amizades (7, acima do mínimo de 5):

Felipe — Gabriel

Gabriel — Helena

Helena — Igor

Igor — Julia

Julia — Kauã

Carla — Helena

Diego — Igor

Rede ampliada

Graus, arestas e densidade

Usuário	Grau

Kauã	3
Bruno	3
Carla	4
Diego	4
Elisa	3
Felipe	3
Gabriel	2
Helena	3
Igor	3
Julia	2

Soma dos graus: 3+3+4+4+3+3+2+3+3+2 = 30

Arestas: 30 ÷ 2 = 15 (as 8 originais + 7 novas ✔)

Densidade: D = 2 × 15 / (10 × 9) = 30 / 90 = 0,333 = 33,3 %

Comparação das densidades

Usuários	Amizades	Densidade
    
Antes	6-------8-------- 53,3 %

Depois	10------15--------33,3 %

A densidade caiu, embora a rede tenha ganhado amizades. O motivo: o número de pares possíveis cresce com o quadrado dos usuários (de 15 para 45 pares), enquanto as amizades cresceram bem menos (de 8 para 15).


8. Conclusão

O grafo permite descrever a rede ConectaUDF com poucos conceitos: usuários são vértices, amizades são arestas, o grau mede popularidade e a densidade mede o quanto a rede está conectada. Na rede original, de 6 usuários, 53,3 % das conexões possíveis existem e quatro pessoas empatam com grau 3. Ao ampliar a rede para 10 usuários, a densidade caiu para 33,3 %, mostrando que crescer em usuários não significa crescer em coesão. Python automatizou os cálculos (graus, arestas, densidade), encontrou os caminhos mínimos e gerou recomendações de amizade, e seus resultados bateram com os da resolução manual.

9. Pergunta de reflexão

Duas pessoas ainda não são amigas, mas têm três amigos em comum. Como essa informação poderia ser usada para sugerir uma nova conexão?

Três amigos em comum é um sinal forte: a pessoa A e a pessoa B frequentam provavelmente o mesmo círculo (turma, trabalho, bairro). A plataforma pode ordenar as sugestões de A pela quantidade de amigos em comum e mostrar B perto do topo, com a mensagem "3 amigos em comum". Quanto maior o número, maior a chance de a sugestão ser aceita.
