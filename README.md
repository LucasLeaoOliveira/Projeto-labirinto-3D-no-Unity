🎮 Labirinto 3D em Unity

Jogo de labirinto em primeira pessoa desenvolvido na Unity, com geração procedural de paredes, navegação por NavMesh, obstáculos fixos e móveis, regras de proximidade e otimização de desempenho com Occlusion Culling.

O objetivo do jogador é percorrer o labirinto da entrada até a saída sem encostar nas paredes ou nos obstáculos — qualquer aproximação excessiva envia o jogador de volta ao início.


🛠️ Tecnologias


Unity 6.3 LTS (6000.3.17f1)
C#
AI Navigation (NavMeshSurface / NavMeshObstacle)
Occlusion Culling
Textura de tijolo com musgo da Poly Haven
Active Input Handling: Both (compatibilidade com input legado)



🎯 Sobre o projeto

O labirinto é totalmente em 3D e conta com:


Entrada e saída bem definidas
Plataforma inicial antes da entrada e plataforma final após a saída
Mais de 40 paredes geradas proceduralmente
Corredores dimensionados para permitir 1 metro de distância das paredes
Obstáculos fixos e obstáculos móveis
Iluminação configurada e texturas aplicadas em paredes e chão


Regras de gameplay

SituaçãoConsequênciaJogador a menos de 1 metro de uma paredeVolta ao inícioJogador a menos de 0,5 metro de um obstáculoVolta ao inícioJogador alcança a saídaTela de vitória (WINNER)


🎮 Controles

TeclaAçãoW / A / S / DMovimentaçãoMouseOlhar / girar a câmeraFAtiva o modo imortal (desativa as regras de proximidade)GRestaura as regras normais


O modo imortal foi criado para facilitar testes e gravações, permitindo explorar o labirinto sem ser teleportado de volta.




📜 Scripts (C#)

O projeto é organizado em scripts independentes, cada um com uma responsabilidade clara:

MazeBuilder.cs

Geração procedural do labirinto utilizando o algoritmo recursive backtracker, criando paredes finas (thin walls) e definindo a estrutura completa do percurso.

PlayerController.cs

Controle do jogador em primeira pessoa, com movimentação por WASD e câmera controlada pelo mouse, usando o CharacterController.

ProximityChecker.cs

Responsável por aplicar as regras de distância: verifica continuamente a proximidade do jogador em relação às paredes (1m) e aos obstáculos (0,5m), disparando o reset quando os limites são ultrapassados.

GameManager.cs

Gerencia o estado do jogo: lógica de reset, tela de vitória e a detecção automática do ponto inicial (StartPoint) após o labirinto ser reconstruído.

MovingObstacle.cs

Controla os obstáculos móveis com movimento de vai e vem (ping-pong), utilizando NavMeshObstacle com carving para interagir corretamente com a navegação.

GoalTrigger.cs

Detecta quando o jogador alcança a saída e dispara a condição de vitória.

CheatManager.cs

Gerencia o modo imortal: a tecla F desativa as regras de proximidade (sem reconstruir o labirinto) e a tecla G as restaura.


📊 Otimização — Occlusion Culling

O Occlusion Culling impede que o Unity renderize objetos que estão escondidos atrás das paredes e fora do campo de visão do jogador. As paredes foram marcadas como Static e o Bake foi executado pela janela de Occlusion Culling.

O resultado foi uma melhora expressiva de desempenho, medida no mesmo ponto do labirinto:

MétricaSEM OcclusionCOM OcclusionBatches59720SetPass calls58716Triângulos26,1k7,0kVértices43,9k9,0kShadow casters39816FPS84,6 (11,8 ms)104,7 (9,6 ms)

➡️ Redução de aproximadamente 96% nos batches e nas chamadas de renderização, com ganho de cerca de 20 FPS fazendo exatamente a mesma cena.


🚀 Como executar

Pela Unity


Clone este repositório.
Abra o projeto na Unity 6.3 LTS (6000.3.17f1).
Abra a cena principal e clique em Play.


Pelo executável


Acesse a pasta do build (Windows).
Execute o arquivo .exe.



📁 Estrutura do projeto

Labirinto3D/
├── Assets/
│   ├── Scripts/
│   │   ├── MazeBuilder.cs
│   │   ├── PlayerController.cs
│   │   ├── ProximityChecker.cs
│   │   ├── GameManager.cs
│   │   ├── MovingObstacle.cs
│   │   ├── GoalTrigger.cs
│   │   └── CheatManager.cs
│   ├── Materials/
│   ├── Textures/
│   └── Scenes/
├── Packages/
└── ProjectSettings/


As pastas Temp/, Library/ e Obj/ não são incluídas no repositório, pois são geradas automaticamente pela Unity.
