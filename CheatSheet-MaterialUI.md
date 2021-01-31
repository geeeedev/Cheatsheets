## Purpose: Remind myself how to get started with Material UI Core

1. Install dependency
   ```
   cd client
   npm install @material-ui/core
   ```

1. Include Material Design supporting Fonts and Font Icons
   ```html
   <!-- public/index.html -->
   <head>
      <!-- Fonts to support Material Design -->
      <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" />
      <!-- Icons to support Material Design - See Next Bullet -->
      <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
   </head>
   ```

1. Font Icons 
   - use Icon component to activate icon font. The Icon component will display an icon from any icon font that supports ligatures
   - Must include an icon font, e.g. Material icon font via Google Web Fonts:
      `<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />`
   - Wrap the icon name (e.g. "star or bedtime" - font ligature) with Icon component
   - can also apply theme color using color property. By default, an Icon will inherit the current text color. Optionally, you can set the icon color using one of the theme color properties: primary, secondary, action, error & disabled.
   - To find more Material icons and icon names: https://material.io/resources/icons/?style=baseline
      ```js
      import Icon from '@material-ui/core/Icon';
      <Icon>star</Icon>
      <Icon color="primary">shopping_cart</Icon>   //blue shopping cart
      <Icon color="error">bedtime</Icon>           //red-orange moon
      <Icon color="error">face</Icon>              //red-orange moon
      <Icon color="error">tag_faces</Icon>         //red-orange moon
      <Icon color="error" >delete</Icon>           //delete/trashcan icon
      
      ```
   > Icon set the correct class name for the Material icon font. For other fonts, you must supply the class name using the Icon component's className property.


1. makeStyle hook basic
   ```js
   import { makeStyles } from '@material-ui/core/styles';
   
   const useStyles = makeStyles((theme) => ({
      root: {
         '& .MuiTextField-root': {
            margin: theme.spacing(1),
            width: 200,
         }
      },
      buttonStyle:{
         color: "red"
      },
      textStyle:{
         color: "green"
      }
   }));

   export default function App() {
      const classes = useStyle();
      return (
         <>
            <Button className={classes.buttonStyle}>Small Button</Button>
            <h1 className={classes.textStyle}> Text Here </h1>
         </>
      )
   }
   ```

1. makeStyle hook with props with multiple styles applied
   ```js
   //CoolButton.js
   import { makeStyles } from '@material-ui/core/styles';
   import { Button } from "@material-ui/core/Button";
   import classNames from "classnames";   //import classnames@2.2.6 dependencies
   
   const useStyles = makeStyles((theme) => ({
      buttonStyleIMake: props => {        //with "props" needs a return ()
         return {
            color: props.cool ? "blue" : "red".
            [theme.breakpoints.up("sm")]: {     //apply style if screen size is "sm" and up
               color:"green"
            },
            backgroundColor: props.cool ? "orange":"yellow"
         };
      },
      anotherStyle: {
         color: "pink"
      }
   }));

   export default function IconButtonHook(props){
      const classes= useStyle(props);
      return (
         <Button fullWidth className={classNames(classes.buttonStyleIMake,classes.anotherStyle)}> Test Button </Button>;
      )
   }
   ```
   ```js
   //App.js
   import CoolButton from "./CoolButton"

   export default function App() {
      const cool = false;
      return <CoolButton cool={cool} />;
   }
   ```

1. TextField
   ```js
   import TextField from '@material-ui/core/TextField';
   ```

1. Dark Theme with Paper
   - need to import ThemeProvider and createMuiTheme
   - need to create theme with createMuiTheme
   - apply ThemeProvider at the highest/outmost level
   ```js
   import { createMuiTheme, ThemeProvider } from "@material-ui/core/styles";
   ...
   function App() {
      const darkTheme = createMuiTheme({
         palette: {
            type: "dark",
            primary: {
            main: "#ffb74d",
            }
         },
      });

      const lightTheme = createMuiTheme({});
      const [darkMode, setDarkMode] = useState(true);

      return (
         <div className="App">
            <ThemeProvider theme={darkMode ? darkTheme : lightTheme}>
            <Router>
               <Redirect from="/" to="/main" noThrow="true" />
               <Main path="/main" dkMode={darkMode} setDkMode={setDarkMode} />  //use Switch here to change the mode T/F
               <ItemNew path="/freezer/new" />
               <ItemList path="/freezer" />
            </Router>
            </ThemeProvider>
         </div>
      );
   }
   export default App;
   ```
   - Must use Paper component in child components
   - set height to 100vh to apply theme to FULL height page
   ```js
   <Paper style={{height:"100vh"}}>  
      ...
   </Paper>
   ```

1. Link - @reach/router vs. @material-ui
   - set @reach/router Link as a different name, apply into @material-ui Link component={} so we can use both Link features
   - color={} property can be omitted if it's using "primary" since default IS primary
   ```js
   import { Link } from "@material-ui/core";
   import { Link as RouterLink } from "@reach/router";
   ...
   <Link component={RouterLink} to="/main" color="primary">
      Back to Main
   </Link>{" "}|{" "}
   <Link component={RouterLink} to="/freezer" color="seconardy">
      List
   </Link>
   ```

1. Table StickyHeader
   - must use with maxHeight styling
   ```jsx
   const useStyles = makeStyles({
      table: {
         maxWidth: "70%",
         margin: "auto",
         maxHeight: 340,
      },
   });
   ...
      ...
   const ItemList = (props) => {
      const muiClass = useStyles();
      ...
   <TableContainer className={muiClass.table}>
      <Table stickyHeader size="small" >
      <TableHead>
      ...
   }
   ```