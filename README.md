# Criando-um-Player-de-Música-com-React-Native

Desenvolver um player de músicas com React Native envolve várias etapas cruciais, desde a configuração inicial do projeto até a implementação de funcionalidades como reprodução de música, controle de estado do player e navegação entre telas. Vamos estruturar o projeto em módulos para garantir uma organização clara e eficiente.

### Módulos do Projeto

1. **Configuração Inicial do Projeto**
   - Configuração de um novo projeto React Native.
   - Instalação de dependências necessárias (por exemplo, bibliotecas de navegação, biblioteca de áudio).
   - Exemplo de criação de um novo projeto React Native:

   ```bash
   npx react-native init MusicPlayerApp
   cd MusicPlayerApp
   ```

2. **Criação das Telas**
   - Implementação das três telas principais: tela de apresentação (splash screen), tela principal do player e tela da playlist.
   - Utilização de componentes do React Navigation para navegação entre telas.
   - Exemplo de estrutura básica de navegação usando React Navigation:

   ```jsx
   // App.js

   import React from 'react';
   import { NavigationContainer } from '@react-navigation/native';
   import { createStackNavigator } from '@react-navigation/stack';
   import SplashScreen from './screens/SplashScreen';
   import PlayerScreen from './screens/PlayerScreen';
   import PlaylistScreen from './screens/PlaylistScreen';

   const Stack = createStackNavigator();

   function App() {
     return (
       <NavigationContainer>
         <Stack.Navigator initialRouteName="Splash">
           <Stack.Screen name="Splash" component={SplashScreen} />
           <Stack.Screen name="Player" component={PlayerScreen} />
           <Stack.Screen name="Playlist" component={PlaylistScreen} />
         </Stack.Navigator>
       </NavigationContainer>
     );
   }

   export default App;
   ```

3. **Implementação da Tela Principal (Player)**
   - Exibição da música atualmente reproduzida.
   - Controles de reprodução (play, pause, próximo, anterior).
   - Integração com uma biblioteca de áudio como react-native-track-player.
   - Exemplo de código para reproduzir uma música usando react-native-track-player:

   ```jsx
   // PlayerScreen.js

   import React, { useEffect } from 'react';
   import { View, Text, Button } from 'react-native';
   import TrackPlayer from 'react-native-track-player';

   const PlayerScreen = () => {
     useEffect(() => {
       async function setup() {
         await TrackPlayer.setupPlayer();
         await TrackPlayer.add({
           id: '1',
           url: 'https://example.com/music.mp3',
           title: 'Música Exemplo',
           artist: 'Artista Exemplo',
           artwork: 'https://example.com/cover.jpg',
         });
       }
       setup();
     }, []);

     const playMusic = async () => {
       await TrackPlayer.play();
     };

     const pauseMusic = async () => {
       await TrackPlayer.pause();
     };

     return (
       <View>
         <Text>Player Screen</Text>
         <Button title="Play" onPress={playMusic} />
         <Button title="Pause" onPress={pauseMusic} />
       </View>
     );
   };

   export default PlayerScreen;
   ```

4. **Implementação da Tela da Playlist**
   - Exibição da lista de músicas disponíveis.
   - Navegação para a tela do player ao selecionar uma música.
   - Exemplo básico de lista de músicas em React Native:

   ```jsx
   // PlaylistScreen.js

   import React from 'react';
   import { View, Text, FlatList, TouchableOpacity } from 'react-native';

   const PlaylistScreen = ({ navigation }) => {
     const songs = [
       { id: '1', title: 'Música 1', artist: 'Artista 1' },
       { id: '2', title: 'Música 2', artist: 'Artista 2' },
       { id: '3', title: 'Música 3', artist: 'Artista 3' },
     ];

     const renderItem = ({ item }) => (
       <TouchableOpacity onPress={() => navigation.navigate('Player', { song: item })}>
         <View>
           <Text>{item.title}</Text>
           <Text>{item.artist}</Text>
         </View>
       </TouchableOpacity>
     );

     return (
       <FlatList
         data={songs}
         renderItem={renderItem}
         keyExtractor={(item) => item.id}
       />
     );
   };

   export default PlaylistScreen;
   ```

5. **Estilização e Componentização**
   - Estilização dos componentes para se adequarem ao tema do player de música.
   - Componentização de elementos comuns (botões, cabeçalhos, itens da lista).
   - Exemplo de estilização básica usando StyleSheet do React Native:

   ```jsx
   // Exemplo de estilização em um componente

   import React from 'react';
   import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';

   const MyComponent = () => {
     return (
       <TouchableOpacity style={styles.container}>
         <Text style={styles.text}>Pressione Aqui</Text>
       </TouchableOpacity>
     );
   };

   const styles = StyleSheet.create({
     container: {
       backgroundColor: '#3498db',
       padding: 10,
       borderRadius: 5,
       alignItems: 'center',
     },
     text: {
       color: '#fff',
       fontSize: 16,
     },
   });

   export default MyComponent;
   ```

### Conclusão

Ao seguir este projeto modular para criar um player de músicas com React Native, aprenderemos a configurar um projeto, implementar navegação entre telas, reproduzir músicas utilizando bibliotecas específicas e criar uma interface de usuário funcional e agradável. Certifique-se de adaptar os exemplos e a estrutura do projeto às suas necessidades específicas, explorando as funcionalidades adicionais que o React Native oferece para criar aplicativos móveis interativos e eficientes.
