# debug
        iOS cmd+d remote JS Debuggin
        

# layout

        default: upper left
        
        justifyContent: 'flex-start' // upper left same as default
                        'flex-end'  // vertical bottom position in container
                        'center'    // center vertically in container
                        
                        
        alignItems: 'flex-start'
                    'center'
                    'flex-end'
                    
        height: 60,
        paddingTop: 15,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.2,
        elevation: 2,
        position: 'relative'



# passing data : a lot create an instance and set value in Swift/Objc
        //index.js
        
        const App = () => <Header headerText={'Erics Albums'} />;
        
        //header.js
         const Header = props => {
          const { textStyle } = styles;
          return (
            <View style={styles.viewStyle}>
              <Text style={textStyle}>{props.headerText}</Text>;
            </View>
           );
          };
          
          
