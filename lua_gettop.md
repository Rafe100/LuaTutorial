# lua_gettop
### 获取函数参数数量
```
LUA_API int lua_gettop (lua_State *L) {
  return cast_int(L->top - (L->ci->func + 1));
}
```