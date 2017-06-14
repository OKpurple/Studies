JSTL 리스트 카운트 표시

<c:set value="${list.size()}" var="listCnt"></c:set>



JSTL 조건문

<c:if test="${listCnt == listStatus.index }">

</c:if>



JSTL if, else 조건문

<c:choose>

	<c:when test="${listCnt > 0}">

		<c:forEach items="${list}" var="listItem" varStatus="listStatus">

			listItem.title, listItem.content

		</c:forEach>

	</c:when>

	<c:otherwise>

		게시물이 없습니다.

	</c:otherwise>

</c:choose>



  <c:choose>

        <c:when test="${results.totalAns ne 0}">

            <fmt:formatNumber value="${results.totalSec / results.totalAns }" maxFractionDigits="3" />

        </c:when>

        <c:otherwise>

            0

        </c:otherwise>

    </c:choose>



JSTL formatter

<fmt:parseDate  type="date" value="${listItem.regDt }" var="regDt" pattern="yyyyMMddHHmmss"/>

<fmt:formatDate value="${regDt}" pattern="yyyy-MM-dd HH:mm" />



출처: http://devzeroty.tistory.com/entry/JSTL-JSTL-필수-문법 [Dev Story..]