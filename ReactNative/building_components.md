        //import library
        import React from 'react';
        import { Text } from 'react-native';
        //make component

        const Header = () => {
          const { textStyle } = styles;  //set property
          return <Text style={textStyle}>Eric Alubms!</Text>;
        };

        const styles = {  //style
          textStyle: {
            fontSize: 20
          }
        };

        //make component available to other parts of the app
        export default Header;
