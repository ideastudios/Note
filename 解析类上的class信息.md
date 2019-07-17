    private Class<?> getType(Object object){
        Type genericType = object.getClass().getGenericSuperclass();
        Type[] actualTypeArguments = ((ParameterizedType) genericType).getActualTypeArguments();
        return(Class<?>)actualTypeArguments[0];
    }
    
    public abstract class CallBack<T>{
        public abstract void onResult(T t);
    }
    
    public class MyCallback extends CallBack<Student>{

        @Override
        public void onResult(Student student) {
            
        }
    }
