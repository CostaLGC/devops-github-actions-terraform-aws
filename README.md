# DevOps GitHub Actions Terraform AWS

Automatize e gerencie sua infraestrutura na AWS com GitHub Actions e Terraform! Este repositório oferece workflows prontos para uso que integram poderosas ferramentas de automação, permitindo que você provisione e gerencie recursos na nuvem de forma eficiente.

## Recursos

- Projetado para acelerar o desenvolvimento e a entrega contínua (CI/CD).
- Configuração fácil e pronta para uso com Terraform e AWS.
- Fluxos de trabalho personalizáveis para atender às suas necessidades específicas de DevOps.
- Ensina boas práticas para aplicação e remoção de recursos com Terraform, incluindo etapas detalhadas para o `apply` e o `destroy`.
- Utiliza um provider Terraform para se conectar à AWS e gerenciar recursos na nuvem.

## Como Usar

1. Faça um fork deste repositório.
2. Clone o fork para o seu ambiente local.
3. Configure as variáveis de ambiente necessárias no GitHub.
4. Personalize os workflows conforme necessário para o seu projeto.

## Configuração do Provider

A primeira etapa ao trabalhar com Terraform é a configuração do provider, responsável por comunicar-se com o provedor de nuvem (no nosso caso, a AWS) e realizar operações nos recursos. Para isso, utilizamos o bloco `provider` no código Terraform. 

No Terraform, o provedor (`provider`) é uma parte fundamental que estabelece a conexão com um provedor de nuvem, como a AWS, Azure, Google Cloud, entre outros. Para que o Terraform possa interagir com a infraestrutura na nuvem, é necessário configurar corretamente o provedor, o que inclui fornecer credenciais de acesso.

As credenciais de acesso são necessárias para autenticar-se na nuvem e realizar operações nos recursos. No caso específico da AWS, as credenciais de acesso são geralmente compostas por um ID de chave de acesso (`Access Key ID`) e uma chave de acesso secreta (`Secret Access Key`).

Essas credenciais podem ser configuradas de várias maneiras, incluindo o uso de arquivos de configuração locais, variáveis de ambiente, ou, em ambientes de nuvem, associando uma IAM Role à instância onde o Terraform está sendo executado.

Veja um exemplo:

```hcl
provider "aws" {
  region = "us-east-1"
}
```
No exemplo abaixo, podemos ver como as credenciais de acesso à AWS são configuradas como variáveis de ambiente em um workflow do GitHub Actions:

```yaml
jobs:
  meu_job:
    runs-on: ubuntu-latest
    env:
      TF_VERSION: "1.0.11"
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

```

## Estado do Terraform

O estado do Terraform - arquivo `terraform.tfstate` - é um arquivo que registra os recursos provisionados e sua configuração atual, permitindo ao Terraform entender e gerenciar as alterações na infraestrutura de forma precisa. Ele rastreia informações como IDs de recursos, metadados e dependências entre os recursos. Este estado é crucial para o Terraform determinar o que precisa ser modificado, criado ou removido em cada execução, garantindo a consistência entre a descrição declarativa no código Terraform e o estado real da infraestrutura na nuvem. O estado do Terraform pode ser armazenado localmente ou em um armazenamento remoto para facilitar o trabalho em equipe e garantir a segurança das informações sensíveis.

O arquivo terraform.tfstate é uma informação sensível e sua exposição pode gerar sérios riscos de segurança. Este arquivo contém detalhes sobre a infraestrutura provisionada, incluindo IDs de recursos, endereços IP e chaves de acesso. Se exposto, um atacante pode usar essas informações para comprometer a segurança da infraestrutura.

Além disso, o arquivo de estado pode conter credenciais de autenticação, como chaves de API e tokens de acesso, que, se acessados por terceiros não autorizados, podem ser explorados para ganhar acesso não autorizado à infraestrutura.

Para proteger o arquivo de estado do Terraform, é essencial armazená-lo de forma segura, limitar o acesso apenas a membros autorizados da equipe e evitar a exposição acidental. Recomenda-se o uso de serviços de armazenamento na nuvem com controle de acesso adequado ou soluções de gerenciamento seguro de segredos, como o Vault da HashiCorp.

Em resumo, proteger o arquivo de estado do Terraform é fundamental para garantir a segurança da infraestrutura na nuvem e prevenir potenciais violações de segurança.

## Contribuindo

Sinta-se à vontade para contribuir com melhorias, correções de bugs ou novos recursos! Basta abrir uma issue ou enviar uma pull request.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
