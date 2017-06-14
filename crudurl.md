###유저등록하는 html페이지###
`http://13.124.115.238:8080/insertUser`

###글등록하는 html페이지 (user_id:7로만 전송###
`http://13.124.115.238:8080/insertContents`
###GET 모든유저보기##
`http://13.124.115.238:8080/user`
###GET 모든글보기
`http://13.124.115.238:8080/contents`

_res.json_

- contents의 모든속성
- user_info.user_name

###POST user_id인 사람 글쓰기###
`http://13.124.115.238:8080/contents/:id`

_req.body_

- content_text
- share_range
- location_range
- has_image
	- 0 : 이미지 없음
	- 1 : 이미지 첨부함

###PUT
`PUT http://13.124.115.238:8080/contents/:contents_id`

- req.body post와 동일
- 이미지 없던 글에서 이미지 있는 글로 업데이트 하는거 아직안함

###DELETE
`DELETE http://13.124.115.238:8080/contents/:contents_id`
