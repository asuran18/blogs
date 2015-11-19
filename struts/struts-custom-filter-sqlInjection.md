# struts 自定义拦截器 - 过滤SQL注入 #

####自定义拦截器代码

	com.test.filter

	import java.util.Iterator;
	import java.util.Map;
	import java.util.Map.Entry;

	import com.opensymphony.xwork2.ActionContext;
	import com.opensymphony.xwork2.ActionInvocation;
	import com.opensymphony.xwork2.interceptor.AbstractInterceptor;
	import com.opensymphony.xwork2.util.ValueStack;

	public class IllegalCharacterInterceptor extends AbstractInterceptor {

		@Override
		public String intercept(ActionInvocation invocation) throws Exception {
			// 通过核心调度器invocation来获得调度的Action上下文
			ActionContext actionContext = invocation.getInvocationContext();
			// 获取上下文的请求参数
			Map valueTreeMap = actionContext.getParameters();
			// 获得请求参数集合的迭代器
			Iterator iterator = valueTreeMap.entrySet().iterator();
			while (iterator.hasNext()) {
				// 获得迭代的键值对
				Entry entry = (Entry) iterator.next();
				// 获得键值对中的键值
				String key = (String) entry.getKey();
				if("name".equals(key) || "pwd".equals(key)) { //如果包含"'"字符，直接拦截
					String[] val = (String[])entry.getValue();
					for(int i = 0; i < val.length; i++) {
						if(val[i].contains("'")) {
							return null;
						}
					}
				}
			}
			String result = null;
			try {
				// 调用下一个拦截器，如果拦截器不存在，则执行Action
				result = invocation.invoke();
			} catch (Exception e) {
				e.printStackTrace();
			}
			return result;
		}
	}

####struts.xml配置

	//...其他配置...
	<interceptors>
		//... 其他拦截器 ...
		<interceptor name="illegalCharacter" class="com.test.filter.IllegalCharacterInterceptor"/>

		<interceptor-stack name="test">
			<interceptor-ref name="defaultStack" ></interceptor-ref>
			<interceptor-ref name="illegalCharacter" />
			//... 其他拦截器引用 ...
		</interceptor-stack>
	</interceptors>
	<!-- 设置为默认拦截器栈 -->
	<default-interceptor-ref name="test" />