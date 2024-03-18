# Atividade 03b

## Visual Studio 2019 e Docker

Seguir os passos descritos no documento:

[Quickstart: Docker in Visual Studio](https://docs.microsoft.com/pt-br/visualstudio/containers/container-tools?view=vs-2019) 


Teste o debug da aplicação colocando um break point na action que devole a view do Home.

Agora baixe o projeto abaixo do GitHub, crie a base de dados no SQL Server local e habilite o Docker no projeto e execute o serviço no Docker. 

https://github.com/renatogroffe/ASPNETCore2.2_SQLServer-JSON


Se a configuração do SQL do host não permitir conexões remotas pode surgir o erro abaixo no console do Docker no momento da execução da API.

```bash
fail: Microsoft.AspNetCore.Server.Kestrel[13]
      Connection id "0HLNTHL3BF486", Request id "0HLNTHL3BF486:00000001": An unhandled exception was thrown by the application.
System.Exception: GXApplication exception ---> System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> GeneXus.Data.GxADODataException: Type:GeneXus.Data.GxADODataException.A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. 
```
Um dos motivos pode ser porque o SQL Server não está configurado para receber conexões remotas via IP. Para configurar isso seguir as indicações do documento abaixo:

- [Configurando o SQL Server para Acesso Remoto](http://www.regilan.com.br/wp-content/uploads/2015/11/ROTEIRO-Configurando-o-SQL-Server-para-Acesso-Remoto.pdf)

Se mesmo com essa configuração o erro persistir, edite a propriedade Server Name na string de conexão colocando **host.docker.internal** no lugar do IP ou nome da máquina. Após isso dê build e faça novamente o deploy para o Docker pela opção Deploy Application do menu Build.

Próximo: [Atividade 04](04-atividade.md)