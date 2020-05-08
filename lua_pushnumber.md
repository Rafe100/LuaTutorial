
```
LUA_API void lua_pushnumber (lua_State *L, lua_Number n) {
  lua_lock(L);
  setfltvalue(L->top, n);
  api_incr_top(L);
  lua_unlock(L);
}

#define setfltvalue(obj,x) { TValue *io=(obj); val_(io).n=(x); settt_(io, LUA_TNUMFLT); }

#define val_(o)		((o)->value_)

/*
** Union of all Lua values
*/
typedef union Value {
  GCObject *gc;    /* collectable objects */
  void *p;         /* light userdata */
  int b;           /* booleans */
  lua_CFunction f; /* light C functions */
  lua_Integer i;   /* integer numbers */
  lua_Number n;    /* float numbers */
} Value;

/* type of numbers in Lua */
typedef LUA_NUMBER lua_Number;

#define LUA_NUMBER	double
```