# Deber 1 flutter

👋 Nombre: Miguel Muzo

### Resultado del deber 1

Para realizar un widget para mostrar etiquetas solo si MyHomePagetiene al menos 600 píxeles de ancho a utilizar, en este caso, es LayoutBuilder. Le permite cambiar su árbol de widgets dependiendo de cuánto espacio disponible tenga.
```dart
class _MyHomePageState extends State<MyHomePage> {
  var selectedIndex = 0;

  @override
  Widget build(BuildContext context) {
    Widget page;
    switch (selectedIndex) {
      case 0:
        page = GeneratorPage();
        break;
      case 1:
        page = Placeholder();
        break;
      default:
        throw UnimplementedError('no widget for $selectedIndex');
    }

    return LayoutBuilder(builder: (context, constraints) {
      return Scaffold(
        body: Row(
          children: [
            SafeArea(
              child: NavigationRail(
                extended: constraints.maxWidth >= 600,  // ← Here.
                destinations: [
                  NavigationRailDestination(
                    icon: Icon(Icons.home),
                    label: Text('Home'),
                  ),
                  NavigationRailDestination(
                    icon: Icon(Icons.favorite),
                    label: Text('Favorites'),
                  ),
                ],
                selectedIndex: selectedIndex,
                onDestinationSelected: (value) {
                  setState(() {
                    selectedIndex = value;
                  });
                },
              ),
            ),
            Expanded(
              child: Container(
                color: Theme.of(context).colorScheme.primaryContainer,
                child: page,
              ),
            ),
          ],
        ),
      );
    });
  }
}
```
<p align="center"><img src ="https://user-images.githubusercontent.com/74844624/213601240-09b80044-93cb-4622-8f58-475448f2c88f.png" width="700"/></p>

Luego se crea una nueva pantalla para realizar el cambio de una ventana a otra, la página creada tiene la funcionalidad de agregar los nombres favoritos, que se emiten aleatoriamente, el cual se agrega solo si se aplasto el botón de me gusta.

```dart
class FavoritesPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var appState = context.watch<MyAppState>();

    if (appState.favorites.isEmpty) {
      return Center(
        child: Text('No favorites yet.'),
      );
    }

    return ListView(
      children: [
        Padding(
          padding: const EdgeInsets.all(20),
          child: Text('You have '
              '${appState.favorites.length} favorites:'),
        ),
        for (var pair in appState.favorites)
          ListTile(
            leading: Icon(Icons.favorite),
            title: Text(pair.asLowerCase),
          ),
      ],
    );
  }
}
```

<p align="center"><img src ="https://user-images.githubusercontent.com/74844624/213601574-4098b29f-043b-4bc8-abc9-5d213c0caf49.png" width="250" height="500"/></p>

Una vez definida la nueva pantalla se realiza el llamado mediante una sentencia switch el cual redirige a la nueva pantall denominada favoritas.

<p align="center"><img src ="https://user-images.githubusercontent.com/74844624/213603256-8ec1ee7d-46bd-4adf-890b-bec0b61c6603.png" width="450"/></p>

### Evidencia del desarrollo del debber

<p align="center"><img src ="https://user-images.githubusercontent.com/74844624/213603615-3d92969a-18a5-43dc-8f4a-35498a21d2ce.png" width="450"/></p>


