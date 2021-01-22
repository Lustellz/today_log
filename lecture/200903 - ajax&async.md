setAttribute, getAttribute

removeAttribute

- 엘리먼트 복사, 이동

부모-자식 관계: `parent.append(child-contents)`기준점 뒤, `parent.prepend(child-contents)`기준점 앞

형제 관계: `sibling.before(new-sibling)`기준점 앞, `sibling.after(new-sibling)`기준점 뒤

자식-부모 관계: `child-contents.appendTo(parent)`기준점 뒤, `child-contents.prependTo(parent)`기준점 앞

형제 관계: `new-sibling.insertBefore(sibling)`기준점 앞, `new-sibling.insertAfter(sibling)`기준점 뒤

집합인데 각각의 작업이 다름: each

get, post 방식으로 요청: xml으로 response 받음

getJson 방식으로 요청: json으로 response 받음

+ java.io.File.separator(아 이거는... 제 과제요...)

each, find(<-자식으로 접근 xml에서 사용)