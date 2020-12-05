# 🧩 Tab Menu
![Tabs](.%5B20201205%5D_component_tab_menu_images/e523e623.png)

## Code
```jsx
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
    display: inline-block;
    width: 100%;
    height: 100%;

    ul {
    	display: table;
    	margin: 0;
    	padding: 0;
    	width: 100%;
    	list-style: none;
    	cursor: pointer;
    }
    li {
    	float: left;
    	margin: 0;
    	padding: 8px 20px;
    	background-color: #ffffff;
    	opacity: 0.5;
    }

    .active {
    	font-weight: bold;
    	opacity: 1;
    }
`;
const Section = styled.div`
    padding: 20px;
    background-color: #ffffff;
`;

const Tabs = ({ menus, content }) => {
    const [active, setActive] = React.useState(1);

    const handleChangeTabMenu = (e) => {
    	const id = parseInt(e.target.id);
    	setActive(id);
    };

    return (
        <Container>
            <ul onClick={handleChangeTabMenu}>
                {menus.map((menu) => (
                    <li
                        key={menu.id}
                        id={menu.id}
                        className={menu.id === active ? 'active' : ''}
                    >
                        {menu.name}
                    </li>
                ))}
            </ul>
            <Section>{content}</Section>
        </Container>
    );
};

export default Tabs;
```

## Usage
```jsx
import React from 'react';
import Tabs from '../components/Tabs';
import styled from 'styled-components';

const Container = styled.div`
    padding: 20px;
    background-color: #7b7b7b;
`;
const menus = [
    { id: 1, name: '메뉴1' },
    { id: 2, name: '메뉴2' },
    { id: 3, name: '메뉴3' },
];
const content = '내용';

const ExampleTabs = () => {
    return (
        <Container>
        	<Tabs menus={menus} content={content} />
        </Container>
    );
};

export default ExampleTabs;
```
