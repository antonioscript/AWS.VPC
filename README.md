# AWS.VPC
Theoretical repository on how VPC works in AWS

# Introdução à VPC na AWS

## O que é VPC?

**VPC (Virtual Private Cloud)** é uma rede privada isolada dentro da AWS, onde você pode lançar recursos da nuvem como EC2, RDS, Lambda, etc. Você controla totalmente:

- Faixas de IP
- Sub-redes
- Roteamento
- Firewalls (Security Groups e NACLs)
- Conectividade com a internet e redes locais

---

## Componentes Fundamentais da VPC

### 1. CIDR Block
Define a faixa de IPs da sua VPC. Exemplo:

_10.0.0.0/16_

Permite até 65.536 endereços IPs.

---

### 2. Subnets

Sub-redes dentro da VPC. Podem ser:

- **Public Subnet** – com acesso à internet
- **Private Subnet** – sem acesso direto à internet

Exemplo:
</br>

_Public: 10.0.1.0/24_

_Private: 10.0.2.0/24_


---

### 3. Internet Gateway (IGW)

Permite que instâncias em subnets públicas se comuniquem com a internet.

---

### 4. Route Tables

Define regras de roteamento. Associada a subnets para definir como o tráfego deve ser direcionado.

---

### 5. NAT Gateway

Permite que instâncias em subnets privadas **acessem a internet** (ex: para atualizações), sem serem acessíveis de fora.

---

### 6. Security Groups vs NACLs

- **Security Groups**: Firewall por instância (ex: EC2). Stateful.
- **NACLs (Network ACLs)**: Firewall por subnet. Stateless.

---

## Exemplo de Arquitetura

1. Criar VPC com `10.0.0.0/16`
2. Criar duas subnets:
   - Pública: `10.0.1.0/24` (servidores web)
   - Privada: `10.0.2.0/24` (banco de dados)
3. Associar um Internet Gateway à VPC
4. Criar uma tabela de rotas para a subnet pública apontando para o IGW
5. Criar um NAT Gateway na subnet pública
6. Configurar a rota da subnet privada para passar pelo NAT Gateway
7. Usar Security Groups e NACLs para proteger os recursos

---


