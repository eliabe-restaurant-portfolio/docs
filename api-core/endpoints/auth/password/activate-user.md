# **Endpoint: `POST /api/users/reset-password`**

Ativa um usuário inativo e redefine sua senha. Para que a operação seja bem-sucedida, o usuário precisa fornecer o token e o hash de verificação que foram previamente enviados (geralmente por e-mail, após solicitar a redefinição de senha ou criar usuário).

Somente é permitido acessar esse endpoint usuário inativo.

Caso seja verificado que o reset de senha se expirou, ou seja, já se passou mais de 30 minutos desde a criação do reset, este será deletado logicamente.

Só será possível ativar o usuário se o código de confirmação enviado pelo usuário for compatível com o encriptado no banco de dados.

Caso o código seja compatível, o usuário é ativado com a nova senha e reset é deletado logicamente.

## **Requisição**

  * **Método:** `POST`

  * **URL:** `/api/api/auth/activate`

  * **Headers:**

      * `Content-Type: application/json`

  * **Corpo da Requisição (Body):**

      * É necessário enviar o token de redefinição de senha, o hash de verificação e a nova senha desejada.

    **Exemplo:**

    ```json
    {
        "reset_password_token": "2f99f0b7-6a94-461d-bfed-6f3c6174a2cc",
        "reset_password_hash": "siAnorktzpgpvjwa",
        "new_password": "#SenhaForte123"
    }
    ```

## **Respostas**

### **`200 OK` - Sucesso**

Retornado quando a senha do usuário é alterada com sucesso.

  * **Corpo (Body):**
    ```json
    {
        "success": true,
        "message": "password updated successfully",
        "data": null,
        "code": 200,
        "errors": []
    }
    ```

### **`400 Bad Request` - Reset de senha não existe internamente**

Isso pode acontecer porque o usuário enviou token errado ou o reset de senha já foi excluido.

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "reset password not exists",
        "data": null,
        "code": 400,
        "errors": ["bad request"]
    }
    ```

### **`400 Bad Request` - Reset de senha não existe internamente**

Isso pode acontecer porque o usuário enviou token errado ou o reset de senha já foi excluido.

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "reset password not exists.",
        "data": null,
        "code": 400,
        "errors": ["bad request"]
    }
    ```

### **`400 Bad Request` - Usuário já é ativo**

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "user is already active.",
        "data": null,
        "code": 400,
        "errors": ["bad request"]
    }
    ```

### **`400 Bad Request` - Usuário é bloqueado**

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "user is blocked.",
        "data": null,
        "code": 400,
        "errors": ["bad request"]
    }
    ```

### **`400 Bad Request` - Token inválido**

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "token invalid.",
        "data": null,
        "code": 400,
        "errors": ["bad request"]
    }
    ```
    