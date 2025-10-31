# Gerenciando Instancias EC2 na AWS - Desafio 1

# Cenário Fictício: Aplicação de Streaming de Conteúdo Multimídia :câmera_de_cinema::nota_musical:
Nesse material estou enviando o primeiro desafio, com uma arquitetura desenhada no draw.io.

O Objetivo desse desafio era realizar e criar uma arquitetura 

Nessa aplicação foi considerado a ideia de uma arquitetura de conteúdo multimídia (vídeos, músicas ou ambos) sob demanda para usuários. 

Os arquivos de mídia são armazenados em Amazon S3, enquanto os servidores em Amazon EC2 gerenciam as requisições e processam os dados.

# Arquitetura Proposta :lâmpada:
1. Amazon S3: Armazenamento de Conteúdo
   - Todos os arquivos multimídia (vídeos, músicas, imagens) ficam armazenados no Amazon S3.
   - O bucket S3 é configurado para:
     - Entrega otimizada de conteúdo via Amazon CloudFront (rede CDN), garantindo baixa latência para os usuários.
     - Controle de acesso via políticas de bucket e/ou links assinados para proteger conteúdo sensível.
2. Amazon EC2: Backend e Processamento
   - Servidores EC2 são configurados como o backend principal que:
     - Gerencia requisições dos usuários finais.
     - Faz transcodificação de mídia sob demanda (por exemplo, ajusta resolução de um vídeo para compatibilidade com dispositivos).
     - Valida autenticações e autorizações de usuários.
3. Camada de Aplicação (Web/App Server)
   - Aplicação Web (ou App Mobile) que os usuários acessam para buscar e assistir o conteúdo.
   - As interfaces de usuário podem ser hospedadas em:
     - EC2 (se usar um framework/aplicação própria).
     - Amazon Elastic Beanstalk (se preferir abstrair parte da gestão dos servidores).
4. CloudFront para Distribuição Global
   - O S3 é integrado ao Amazon CloudFront, uma CDN, para distribuir o conteúdo multimídia com desempenho otimizado em regiões do mundo todo.
5. Amazon RDS ou DynamoDB: Gerenciamento de Dados do Usuário
   - O EC2 utiliza um banco de dados, como:
     - Amazon RDS (relacional, por exemplo: MySQL/Postgres) para manter informações relacionadas a contas, histórico de consumo, ou preferências do usuário.
     - Amazon DynamoDB (não-relacional, escalável) para armazenar dados de sessões e cache.
6. Escalabilidade e Alta Disponibilidade
   - Utilização de Auto Scaling Groups para os servidores EC2, ajustando a capacidade conforme a carga aumenta ou diminui.
   - Elastic Load Balancer (ELB) para distribuir o tráfego entre as instâncias EC2.
7. Segurança
   - Buckets S3 com controle de acesso rígido (ex.: objetos apenas acessíveis via links assinados).
   - EC2 em uma VPC (Virtual Private Cloud) com sub-redes públicas/privadas para maior controle de isolamento.
   - AWS IAM para gerenciar permissões e acesso a serviços.
8. Monitoramento e Logs
   - Logs de acesso ao S3 via Amazon CloudWatch.
   - Os servidores EC2 monitorados também pelo CloudWatch, com alertas configurados para CPU, memória e outros eventos críticos.
