Objetivo: Desconstruir, entender e aprimorar a aplicação de portal de hotéis, dominando os conceitos de Rails, a estrutura de código e as gems profissionais utilizadas.

Módulo 1: Configuração e Arquitetura do Projeto

O primeiro passo é entender como o projeto está montado e como fazê-lo funcionar na sua máquina.

    Ambiente de Desenvolvimento:

        Analisar o Gemfile: Quais são as principais gems do projeto? Identifique as gems para: autenticação (devise), manipulação de dinheiro (money-rails), paginação (pagy), e formulários (simple_form). Por que cada uma delas foi escolhida?

        Configuração do Banco de Dados (config/database.yml): Veja como o arquivo está configurado para usar PostgreSQL. Qual a vantagem de usar variáveis de ambiente (ENV) para as credenciais do banco?

        Scripts de Setup (bin/setup e Rakefile): Investigue o arquivo lib/tasks/dev.rake. O que a tarefa dev:reset faz? Por que ela é útil para o desenvolvimento?

        Execução: Siga as instruções do README.md para rodar o projeto localmente com bundle install e ./bin/dev.

    Estrutura de Rotas (config/routes.rb):

        O que são namespaces? Por que o projeto está dividido nos namespaces :admin e :client?

        Como o Devise é configurado para ter rotas de login diferentes para admin e client?

        O que a rota root "welcome#index" significa?

Módulo 2: Autenticação e Autorização com Devise

Seu projeto tem uma separação clara entre o que um administrador e um cliente podem fazer.

    Modelo User (app/models/user.rb):

        Como o enum role funciona para definir os papéis de client e admin?

        Quais validações estão presentes no modelo de usuário?

    Controllers do Devise:

        Analise os controllers em app/controllers/users/. Por que foi necessário criar controllers customizados (sessions_controller.rb, registrations_controller.rb)?

        Como o after_sign_in_path_for no sessions_controller.rb direciona o usuário com base na sua role?

Módulo 3: Lógica de Negócio - Painel do Administrador

Esta é a área onde a gestão do portal acontece.

    Models Principais (app/models/):

        hotel.rb: Quais são as associações (has_many, has_and_belongs_to_many)? O que o after_create :create_rooms faz e por que é uma automação poderosa?

        room.rb: Como o escopo available_between funciona para encontrar quartos disponíveis? É uma das lógicas mais importantes do sistema.

        block_room.rb: Analise a validação no_conflicting_reservations_or_blocks. Como ela impede que um quarto seja bloqueado se já houver uma reserva?

    Controllers de Admin (app/controllers/admin/):

        hotels_controller.rb: Como a gem Pagy é utilizada para paginar a lista de hotéis?

        rooms_controller.rb: Observe o método update_multiple. Como ele permite atualizar vários quartos de uma só vez a partir de um formulário?

Módulo 4: Lógica de Negócio - Fluxo do Cliente

Esta é a experiência do usuário final, desde a busca até a reserva.

    Form Objects (app/forms/):

        O projeto usa ReservationForm e PaymentForm. Por que usar um "Form Object" (uma classe que não herda de ApplicationRecord) em vez de salvar os dados diretamente no modelo Reservation?

        Como a sessão (session) é usada nos controllers reservations_controller.rb e payments_controller.rb para passar dados entre os passos da reserva?

    Serviços (app/services/):

        Qual é a responsabilidade da classe Hotels::GetRoomPriceDescription? Por que é uma boa prática extrair essa lógica para uma classe de serviço em vez de colocá-la no controller ou no model?

    Mailers (app/mailers/):

        Analise o reservation_mailer.rb. Como ele envia e-mails de confirmação e cancelamento? O que o método deliver_later faz?

Módulo 5: Frontend com Bootstrap e Stimulus

A interface do usuário é construída com ferramentas modernas do ecossistema Rails.

    CSS com Bootstrap (application.bootstrap.scss):

        Navegue pelas views em app/views/. Identifique como as classes do Bootstrap (ex: card, btn, container) são usadas para estruturar o layout.

        O que o arquivo _variables.scss permite fazer?

    JavaScript com Stimulus (app/javascript/controllers/):

        payment_controller.js: Como este controller gerencia a exibição dos campos de formulário de acordo com o método de pagamento selecionado (Cartão de Crédito, Boleto, PIX)?

        search_rooms_controller.js: Como ele busca dinamicamente os quartos disponíveis sem recarregar a página, usando Turbo Streams?

Módulo 6: Gems Profissionais e Próximos Passos

Seu projeto já utiliza gems que são padrão na indústria.

    Money-Rails: Como essa gem ajuda a evitar problemas de arredondamento com valores monetários? Veja seu uso nos modelos Reservation e Payment.

    Simple Form: Compare um formulário feito com simple_form (ex: app/views/admin/hotels/_form.html.erb) com um formulário padrão do Rails. Quais as vantagens?

    Pagy: Além dos controllers, veja como a view pagy_bootstrap_nav é chamada para renderizar a navegação da página.

    Docker (Dockerfile): O projeto inclui um Dockerfile. Qual é o objetivo dele? (Dica: é para criar um ambiente padronizado para produção).

Próximo Passo Sugerido: Tente adicionar uma nova funcionalidade do zero, como um sistema de avaliações (reviews) para os hotéis, seguindo a arquitetura e os padrões que você estudou neste guia.

Use este prompt como um roteiro. Explore cada módulo, faça anotações e, o mais importante, tente modificar o código e ver o que acontece. Parabéns pelo excelente projeto!
