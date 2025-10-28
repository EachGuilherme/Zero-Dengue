# 🦟 ZeroDengue ZL

## Visão Geral do Projeto

O **ZeroDengue ZL** é um projeto de iniciativa cívica e tecnológica desenvolvido para auxiliar no combate e prevenção da proliferação do mosquito *Aedes aegypti*, vetor da dengue, zika e chikungunya, na Zona Leste de São Paulo (ZL).

Este projeto visa ser uma ponte entre a população e a ação preventiva, permitindo que os cidadãos denunciem de forma rápida e eficiente os pontos de concentração e possíveis criadouros do mosquito em suas comunidades. Ao centralizar essas informações, a plataforma contribui para que as autoridades de saúde e a própria população possam se prevenir e agir de forma mais localizada e eficaz.

### Principais Funcionalidades

| Funcionalidade | Descrição | Status de Implementação |
| :--- | :--- | :--- |
| **Página Inicial** (`index.html`) | Apresenta a missão do projeto e um resumo de como realizar denúncias. | Completo (Frontend) |
| **Denúncias** (`denuncias.html`) | Formulário para que o usuário insira informações sobre um possível foco de dengue, incluindo localização (via CEP/Logradouro) e descrição. | Parcial (Frontend completo, **Backend de submissão ausente**) |
| **Informações** (`informacoes.html`) | Conteúdo educativo sobre a dengue, o mosquito *Aedes aegypti*, sintomas, diagnóstico, tratamento e prevenção. | Completo (Frontend) |
| **Estatísticas** (`backend/get_stats.php`) | Script PHP para retornar dados de denúncias por macro-região em formato JSON. | Completo (Backend - Requer MySQL) |

## Tecnologias Utilizadas

O projeto é construído com as seguintes tecnologias:

*   **Frontend:** HTML5, CSS3 (com `style.css`), JavaScript (com `menu.js`).
*   **Design:** Utiliza a biblioteca de ícones [Bootstrap Icons](https://icons.getbootstrap.com/) e a fonte [Poppins](https://fonts.google.com/specimen/Poppins).
*   **Backend (Estatísticas):** PHP e MySQL (para o script `get_stats.php`).
*   **Integração:** Utiliza a API do [ViaCEP](https://viacep.com.br/) para preenchimento automático de endereço no formulário de denúncia.

## Estrutura do Projeto

A organização de arquivos para o GitHub segue a seguinte estrutura:

```
zerodengue/
├── assets/
│   ├── aedess.jpg           # Imagem ilustrativa do Aedes aegypti
│   ├── logosite.png         # Logo do site (versão 1)
│   └── logo-site.png        # Logo do site (versão 2)
├── backend/
│   └── get_stats.php        # Script PHP para buscar estatísticas do banco de dados
├── denuncias.html           # Página com o formulário de denúncia
├── informacoes.html         # Página com informações sobre a dengue
├── index.html               # Página inicial do projeto
├── menu.js                  # Script JavaScript para o menu mobile
├── README.md                # Este arquivo
└── style.css                # Folha de estilos CSS
```

## Como Utilizar (Instalação e Configuração)

Para rodar este projeto localmente, você precisará de um ambiente que suporte **serviço web (HTTP)** e **PHP com MySQL** para o funcionamento completo do backend de estatísticas.

### 1. Clonar o Repositório

```bash
git clone https://github.com/SEU_USUARIO/ZeroDengue.git
cd ZeroDengue
```

### 2. Configuração do Frontend

As páginas HTML (`index.html`, `denuncias.html`, `informacoes.html`) podem ser abertas diretamente no seu navegador, mas o formulário de denúncia e as estatísticas não funcionarão sem o backend.

### 3. Configuração do Backend (Opcional, mas Recomendado)

O projeto requer um servidor web com PHP e um banco de dados MySQL para processar as denúncias e exibir as estatísticas.

#### 3.1. Banco de Dados

O script `backend/get_stats.php` espera uma conexão com um banco de dados MySQL chamado `zero_dengue` e uma tabela `denuncias`.

**Estrutura da Tabela `denuncias` (Exemplo Sugerido):**

```sql
CREATE DATABASE zero_dengue;

USE zero_dengue;

CREATE TABLE denuncias (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cep VARCHAR(9) NOT NULL,
    logradouro VARCHAR(255) NOT NULL,
    subregiao VARCHAR(100) NOT NULL,
    descricao TEXT NOT NULL,
    imagem_url VARCHAR(255),
    data_denuncia TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    macro_regiao VARCHAR(100)
);
```

#### 3.2. Script `get_stats.php`

Você precisará atualizar as credenciais de acesso ao banco de dados no arquivo `backend/get_stats.php`:

```php
// Linha 3 do backend/get_stats.php
$conn = new mysqli("localhost", "username", "password", "zero_dengue"); 
// Altere "username" e "password" pelas suas credenciais.
```

#### 3.3. Submissão de Denúncias

**Atenção:** O arquivo `denuncias.html` aponta para um script de submissão de denúncias que **não está incluso** neste repositório:

```html
<!-- Linha 70 do denuncias.html -->
<form action="http://localhost/ZeroDengue/Denuncia/submit_denuncia.php" method="post">
```

Para que as denúncias funcionem, você precisará criar o script `submit_denuncia.php` que deve:
1.  Receber os dados do formulário (CEP, Logradouro, Subregião, Descrição, Imagem URL).
2.  Validar e sanitizar os dados.
3.  Inserir os dados na tabela `denuncias` do seu banco de dados MySQL.
4.  Redirecionar o usuário para uma página de sucesso ou exibir uma mensagem de erro.

## Contribuições

Contribuições são muito bem-vindas! Se você deseja melhorar o projeto, corrigir bugs ou adicionar novas funcionalidades, siga os passos abaixo:

1.  Faça um **Fork** do projeto.
2.  Crie uma nova *branch* para sua funcionalidade (`git checkout -b feature/nova-funcionalidade`).
3.  Faça suas alterações e *commit* suas mudanças (`git commit -m 'feat: Adiciona nova funcionalidade X'`).
4.  Faça o *push* para a *branch* (`git push origin feature/nova-funcionalidade`).
5.  Abra um **Pull Request** detalhando as alterações.

## Agradecimentos

*   Agradecimento especial ao **ViaCEP** pela API pública de consulta de CEP.

---

**Desenvolvido por:** [Guilherme Ramos de Lima]
**Licença:** [MIT]
