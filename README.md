import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Provide a function to handle named routes. Use this function to
      // identify the named route being pushed, and create the correct
      // Screen.
      onGenerateRoute: (settings){
        // If you push the PassArguments route
        if (settings.name == PassArgumentsScreen.routeName) {
          // Cast the arguments to the correct type: ScreenArguments.
          final ScreenArguments args = settings.arguments;

          // Then, extract the required data from the arguments and
          // pass the data to the correct screen.
          return MaterialPageRoute(
            builder: (context) {
              return PassArgumentsScreen(
                title: args.title,
                message: args.message,
              );
            },
          );
        }
      },
      title: 'O que é Medula Óssea',
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
 

  @override
  Widget build(BuildContext context) {
    var children2 = <Widget>[
            
            // A button that navigates to a named route that. The named route
            // extracts the arguments by itself.
           
            RaisedButton(
              child: Text("Saiba mais"),
              onPressed: () {
                // When the user taps the button, navigate to the specific route
                // and provide the arguments as part of the RouteSettings.
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => ExtractArgumentsScreen(),
                    
                    // Pass the arguments as part of the RouteSettings. The
                    // ExtractArgumentScreen reads the arguments from these
                    // settings.
                    settings: RouteSettings(
                      arguments: ScreenArguments(
                        'Medula Óssea',
                        'A medula óssea, encontrada no interior dos ossos, contém as células-\n tronco hematopoéticas que produzem os componentes do sangue,\n incluindo as hemácias ou glóbulos vermelhos, os leucócitos ou glóbulos\n brancos que são parte do sistema de defesa do nosso organismo, e as\n plaquetas, responsáveis pela coagulação.\n\n Para se tornar um doador de medula óssea é necessário:\n- Ter entre 18 e 55 anos de idade \n-Estar em bom estado de saúde\n- Não ter doença infecciosa transmissível pelo sangue (como infecção pelo HIV ou hepatite)\n-Não apresentar história de doença neoplásica (câncer), hematológica ou autoimune (como lúpus \neritematoso sistêmico e artrite reumatoide)',
                      ),
                    ),
                  ),
                );
              },
            ),
            // A button that navigates to a named route. For this route, extract
            // the arguments in the onGenerateRoute function and pass them
            // to the screen.
            RaisedButton(
              child: Text("Como ajudar?"),
              onPressed: () {
                // When the user taps the button, navigate to a named route
                // and provide the arguments as an optional parameter.
                Navigator.pushNamed(
                  context,
                  PassArgumentsScreen.routeName,
                  arguments: ScreenArguments(
                    'Medula Óssea',
                    '– Procure o hemocentro do seu estado e agende uma consulta de esclarecimento ou palestra sobre doação de medula óssea.\n – O voluntário à doação irá assinar um termo de consentimento livre e esclarecido (TCLE), e preencher uma ficha com informações pessoais.\n Será retirada uma pequena quantidade de sangue (10ml) do candidato a doador.\n É necessário apresentar o documento de identidade.\n – O seu sangue será analisado por exame de histocompatibilidade (HLA), um teste de laboratório para identificar suas características genéticas\n  que vão ser cruzadas com os dados de pacientes que necessitam de transplantes para determinar a compatibilidade.\n – Os seus dados pessoais e o tipo de HLA serão incluídos no Registro Nacional de Doadores Voluntários de Medula Óssea (REDOME).\n – Quando houver um paciente com possível compatibilidade, você será consultado para decidir quanto à doação. \n Por este motivo, é necessário manter os dados sempre atualizados.\n – Para seguir com o processo de doação serão necessários outros exames para confirmar a compatibilidade e uma avaliação clínica de saúde.\n – Somente após todas estas etapas concluídas o doador poderá ser considerado apto e realizar a doação.\n Seja um doador! Tomando essa decisão você poderá mudar histórias! ',
                  ),
                  
                  
                );
              },
            ),
          ];
    return Scaffold(
      appBar: AppBar(
        title: Text('Medula Óssea'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: children2,
        ),
      ),
    );
  }
}

// A Widget that extracts the necessary arguments from the ModalRoute.
class ExtractArgumentsScreen extends StatelessWidget {
  static const routeName = '/extractArguments';

  @override
  Widget build(BuildContext context) {
    // Extract the arguments from the current ModalRoute settings and cast
    // them as ScreenArguments.
    final ScreenArguments args = ModalRoute.of(context).settings.arguments;

    return Scaffold(
      appBar: AppBar(
        title: Text(args.title),
      ),
      body: Center(
        child: Text(args.message),
      ),
    );
  }
}

// A Widget that accepts the necessary arguments via the constructor.
class PassArgumentsScreen extends StatelessWidget {
  static const routeName = '/passArguments';

  final String title;
  final String message;

  // This Widget accepts the arguments as constructor parameters. It does not
  // extract the arguments from the ModalRoute.
  //
  // The arguments are extracted by the onGenerateRoute function provided to the
  // MaterialApp widget.
  const PassArgumentsScreen({
    Key key,
    @required this.title,
    @required this.message,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Text(message),
      ),
    );
  }
}

// You can pass any object to the arguments parameter. In this example,
// create a class that contains both a customizable title and message.
class ScreenArguments {
  final String title;
  final String message;

  ScreenArguments(this.title, this.message);
}
