# Role-based access control

## 배경
- 관리자 웹 프로젝트 진행 중.
- 관리자 권한은 총 3가지가 있고, 각 권한 별로 기능에 대한 접근 제한이 필요하게 됐다.
- 메뉴는 권한에 따라 접근할 수 있도록 해두었는데, 
  뿐만 아니라 페이지 내에서도 각각의 요소 권한을 따로 줘야 하는 경우가 있다.
  
## 권한 분기, 어떤 방법을 사용할까?
- 사용자 정보에 권한에 대한 값을 넣어두고 코드 내에서 if문 내 조건에 권한에 대한 정보를
  하드코딩 하면 되겠지만 아래와 같은 문제가 있을 것으로 예상.
  - 권한이 추가/변경될 경우 모든 조건을 검토하고 필요에 따라 전부 수정해야 한다.
  - 권한이 많을 경우 코드가 지저분해지고 조건을 알아보기 어렵게 된다.
  - 고로 개발자의 많은 에너지가 필요하고 
    버그 발생이나 적절하지 못한 엑세스를 제대로 통제할 수 없을 지 모른다. 
- 기존 코드를 크게 어지럽히지 않으면서 깔끔하게 처리할 수 있는 방법을 고민함.
  - 권한에 대한 조건을 코드 여기저기에 뿌려놓는 게 아니라, 
    추가/수정이 용이하게 한 곳에서 관리할 수 있었으면 좋겠다.
- 그러다가 `Role-based access control`에 대해 알게 됨.

## Role-based access control
```text
In computer systems security, role-based access control (RBAC) or 
role-based security is an approach to restricting system access to authorized users. 
It is used by the majority of enterprises with more than 500 employees,
and can implement mandatory access control (MAC) or discretionary access control (DAC).

Role-based access control (RBAC) is a policy-neutral access-control mechanism 
defined around roles and privileges. The components of RBAC such as role-permissions, 
user-role and role-role relationships make it simple to perform user assignments. 
A study by NIST has demonstrated that RBAC addresses many needs of commercial 
and government organizations. RBAC can be used to facilitate 
administration of security in large organizations with hundreds of users and 
thousands of permissions. Although RBAC is different from MAC and 
DAC access control frameworks, it can enforce these policies without any complication.

* https://en.wikipedia.org/wiki/Role-based_access_control
```

## 예제
### rules.js
- 기능별로 키값을 부여하고 그 키값을 통해 권한을 제어할 것.
- 키값을 정의해둔 파일.
- 권한의 추가/수정/삭제는 모두 이곳에서 이루어진다.
```jsx
export const rules = {
    master: [
    	'AUTH:LOGIN',
    	'AUTH:LOGOUT',
    	'NOTICE:LIST',
    	'NOTICE:CONTENT',
    	'NOTICE:REMOVE',
    	'NOTICE:WRITE',
    	'NOTICE:MODIFY',
    ],
    superAdmin: [
    	'AUTH:LOGIN',
    	'AUTH:LOGOUT',
    	'NOTICE:LIST',
    	'NOTICE:CONTENT',
    	'NOTICE:WRITE',
    	'NOTICE:MODIFY',
    ],
    subAdmin: [
    	'AUTH:LOGIN',
    	'AUTH:LOGOUT',
    	'NOTICE:LIST',
    	'NOTICE:CONTENT',
    ],
};
```

### AuthCheck.js
```jsx
import { rules } from './rules.js';

export const check = (role, code) => {
    const permissions = rules[role];

    if (!permissions) {
    	return false;
    }
    return !!(permissions && permissions.includes(code));
};

const AuthCheck = (props) => {
    return check(props.role, props.code) ? props.yes() : props.no();
};

AuthCheck.defaultProps = {
    yes: () => {
    	return null;
    },
    no: () => {
    	return null;
    },
};

export default AuthCheck;
```
- `role`은 사용자의 권한
- `code`는 `rules.js`에 정의한 키값
- 두 값을 가지고 권한을 체크해서 권한이 있을 경우 props `yes`를, 없을 경우 `no`를 렌더링

### 사용
- 공지사항 삭제는 `master`만 가능한 기능이므로 삭제 버튼을 `master`에게만 보여줘야 함.

#### 기존 코드
```jsx
<ButtonGroup right>
    <Button text='목록' style='infoLine' to={baseURI} />
	<Button
		text='삭제'
		style='primaryLine'
		to={`${baseURI}/write`}
	/>
</ButtonGroup>
```

#### 권한 적용한 수정 후 코드
```jsx
<ButtonGroup right>
    <Button text='목록' style='infoLine' to={baseURI} />
    <AuthCheck
        role={admin.role}
    	code='NOTICE:REMOVE'
    	yes={() => (
            <Button
            	text='삭제'
            	style='primaryLine'
            	to={`${baseURI}/write`}
            />
    	)}
    />
</ButtonGroup>
```

## 작업 후 느낀 생각
- 만약 공지사항 삭제를 `master`뿐 아니라 `superAdmin`에게도 부여하고 싶다면?
- `rules.js`의 `rules['superAdmin']`에 `NOTICE:REMOVE`만 추가해주면 된다.
- 새로운 권한이 추가되더라도 `rules`에 키를 추가하고 값을 정의해놓기만 하면 된다.
- `rules.js`만 잘 관리하면 되는 것.
- 복잡하게 if문을 사용하지 않아도 되고 미리 정의해둔 컴포넌트에 props만 잘 던져주면 되므로
  코드도 생각보다 지저분해지지 않았다.
- 정말 마음에 드는 방식.

##### * Reference : https://auth0.com/blog/role-based-access-control-rbac-and-react-apps/#Role-Based-Access-Control--a-Better-Solution
