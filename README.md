
# Arquitetura Modular Clara MVC (AMC-MVC)

A Arquitetura Modular Clara MVC (AMC-MVC) é baseada nos princípios da arquitetura limpa e utiliza uma estrutura modular que facilita a manutenção, escalabilidade e reutilização de componentes em diferentes projetos. A arquitetura é inspirada no padrão MVC (Model-View-Controller) com módulos adicionais para melhor distribuição de responsabilidades. Tal ideia foi desenvolvida por mim [Mauricio Benjamin da Rocha](https://github.com/mauriciobenjamin700) visando facilitar a manipulação do MVC tradicional.

## Estrutura do Projeto

```plaintext
project/
├── docs/
│   ├── funcionalidades.md
│   ├── regras_de_negocio.md
│   └── manual_usuario.md
├── images/
│   └── (todas as imagens devem estar nesta pasta ou em subpastas da mesma)
├── src/
│   ├── models/
│   ├── views/
│   │   ├── animations/
│   │   ├── colors/
│   │   ├── components/
│   │   ├── fonts/
│   │   ├── scripts/
│   │   └── templates/
│   ├── controllers/
│   │   └── funcs/
│   └── app.py
└── main.py
```

## Diretórios/Arquivos e Suas Responsabilidades

### [`docs`](docs)

Contém toda a documentação do projeto, incluindo mas não se limitando a:

- Documentação de funcionalidades
- Regras de sistema
- Manuais de usuário e desenvolvedor

### [`images`](images)

Contém todas as imagens usadas na aplicação. Todas as imagens devem estar nesta pasta ou em subpastas da mesma.

### [`src`](src)

Contém todo o código-fonte do projeto.

#### [`models`](src/models)

Define os modelos de dados e a lógica de interação com o backend, incluindo:

- Modelos de dados (e.g., classes que representam entidades)
- Interações com o backend (e.g., leitura/escrita de arquivos, comunicação com APIs)

#### [`views`](src/views)

Responsável pela interação do usuário com o sistema. A views é responsavel por arquivos que representam as telas da aplicação, onde cada tela consome de recursos das subpastas para existir.

Organizado em submódulos:

- **animations**: Animações e efeitos visuais da aplicação.
- **colors**: Define a paleta de cores da aplicação.
- **components**: Classes genéricas e/ou pouco modificáveis reutilizadas em diferentes partes da aplicação (e.g., botões padrão, barras de navegação).
- **fonts**: Define as fontes usadas na aplicação.
- **scripts**: Scripts para validação de entrada e saída de dados, garantindo a integridade das interações do usuário.
- **templates**: Itens genéricos que se repetem em várias páginas ou seções da aplicação (e.g., cabeçalhos, rodapés).

#### [`controllers`](src/controllers)

Controladores que manipulam os modelos e as views, garantindo a consistência da interação com o usuário.

Possui apenas um submódulo:

- **funcs**: Funções genéricas que os controladores podem usar frequentemente (e.g., utilitários, conversão de formatos).

### Arquivo [`app.py`](src/app.py)

Ponto de entrada da aplicação, onde os modelos, views e controladores são integrados.

### Arquivo [`main.py`](main.py)

Porto de interação do sistema, onde o app é integrado e inicializado. Aparir do main o usuário navega pelo sistema.

### Princípios da Arquitetura

- **Separação de Responsabilidades**: Cada módulo tem uma responsabilidade clara e definida, facilitando a manutenção e a escalabilidade do projeto.
- **Modularidade**: A aplicação é dividida em módulos independentes que podem ser desenvolvidos, testados e implantados separadamente.
- **Reutilização de Código**: Componentes e funções genéricas são isolados em módulos específicos, permitindo sua reutilização em diferentes partes da aplicação.
- **Flexibilidade**: A estrutura modular facilita a adição de novas funcionalidades e a modificação das existentes sem afetar o restante da aplicação.
- **Facilidade de Testes**: A separação clara entre modelos, views e controladores facilita a criação de testes unitários e de integração.

### Exemplo de Organização de Código

#### `models/example_model.py`

```python
class ExampleModel:
    def __init__(self):
        self.data = []

    def add_data(self, item):
        self.data.append(item)

    def get_data(self):
        return self.data
```

#### `views/main_view.py`

```python
import tkinter as tk
from tkinter import filedialog, messagebox

class MainView(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title('Example Application')
        self.geometry('800x600')
        self.label = tk.Label(self, text='Hello, World!')
        self.label.pack(pady=20)
        self.button = tk.Button(self, text='Click Me', command=self.on_button_click)
        self.button.pack(pady=20)

    def on_button_click(self):
        file_path = filedialog.askopenfilename(title="Select File", filetypes=[("All Files", "*.*")])
        if file_path:
            self.controller.process_file(file_path)

    def set_controller(self, controller):
        self.controller = controller

    def update_label(self, text):
        self.label.config(text=text)
```

#### `controllers/main_controller.py`

```python
class MainController:
    def __init__(self, model, view):
        self.model = model
        self.view = view
        self.view.set_controller(self)

    def process_file(self, file_path):
        self.model.add_data(f'File processed: {file_path}')
        self.view.update_label(f'Data: {self.model.get_data()}')
```

#### `app.py`

```python
from views.main_view import MainView
from controllers.main_controller import MainController
from models.example_model import ExampleModel

def main():
    model = ExampleModel()
    view = MainView()
    controller = MainController(model, view)
    view.mainloop()

if __name__ == '__main__':
    main()
```

### Considerações Finais

A Arquitetura Modular Clara MVC (AMC-MVC) visa proporcionar uma base sólida e flexível para o desenvolvimento de projetos, permitindo que a equipe de desenvolvimento mantenha um código organizado, fácil de manter e escalável. A modularidade e a separação de responsabilidades são pilares fundamentais desta abordagem, facilitando a implementação de novas funcionalidades e a manutenção das existentes.

Este nome reflete tanto a inspiração na arquitetura MVC quanto a ênfase na modularidade e clareza do projeto. Todo o Trabalho citado foi ideaizado visando um desenvolvimento mais organizado e com bons resultados.
