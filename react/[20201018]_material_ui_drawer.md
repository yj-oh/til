# Material-ui Drawer
- 상하좌우 side sheet

### package install
```
npm install @material-ui/core
yarn add @material-ui/core
```

### 예제
![](.%5B20201018%5D_material_ui_drawer_images/e34e1e74.png)

```javascript
import React from 'react';
import styled from 'styled-components';
import Drawer from '@material-ui/core/Drawer';

const Button = styled.button`
    padding:5px;
    margin:10px;
    width:50px;
`;
/* Drawer */
const styles = () => ({
    drawerBackground: {
        backgroundColor:'rgba(0, 0, 0, 0.3)',
    },
    drawerWide: {
        padding:'20px',
        width:'80%',
        textAlign:'center',
    },
});
const StyledDrawer = styled(Drawer)`
    ${({ theme }) => {
        const classes = styles(theme);
        return classes.drawerBackground;
    }};
	
    .MuiDrawer-paper {
        ${({ theme }) => {
            const classes = styles(theme);
            return classes.drawerWide;
        }};
    };
  
    .menu-item {
    	padding:30px;
    	font-size:1.2rem;
    };
`;

const DrawerMenu = () => {
    const menuList = ['Home', 'Board', 'Q&A', 'Help', 'Login'];

    const [state, setState] = React.useState(false);
    const toggleDrawer = (open) => () => {
    	setState(open);
    };

    return (
    	<>
            <Button onClick={toggleDrawer(true)}>메뉴</Button>
            <StyledDrawer
            	anchor='right'
            	open={state}
            	onClose={toggleDrawer(false)}
            >
            	{menuList.map(menu => (
            	    <div className='menu-item'>{menu}</div>
            	))}
            </StyledDrawer>
        </>
    );
};

export default DrawerMenu;
```

##### * Reference : https://material-ui.com/components/drawers/
