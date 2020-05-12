
在luaState的top设置number值，top指针增加
具体的number数值设置在value_中，而tt_中的是类型值
```
LUA_API void lua_pushnumber (lua_State *L, lua_Number n) {
  lua_lock(L);
  setfltvalue(L->top, n);
  api_incr_top(L);
  lua_unlock(L);
}

#define setfltvalue(obj,x) { TValue *io=(obj); val_(io).n=(x); settt_(io, LUA_TNUMFLT); }

#define TValuefields	Value value_; int tt_

typedef struct lua_TValue {
  TValuefields;
} TValue;

#define val_(o)		((o)->value_)

#define settt_(o,t)	((o)->tt_=(t))

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

//luaState 的top指针增加
#define api_incr_top(L)   {L->top++; api_check(L, L->top <= L->ci->top, "stack overflow");}

//lua中关于各种类型的定义
#define LUA_TNUMFLT	(LUA_TNUMBER | (0 << 4))  /* float numbers */
#define LUA_TNUMINT	(LUA_TNUMBER | (1 << 4))  /* integer numbers */

#define LUA_TNIL		0
#define LUA_TBOOLEAN		1
#define LUA_TLIGHTUSERDATA	2
#define LUA_TNUMBER		3
#define LUA_TSTRING		4
#define LUA_TTABLE		5
#define LUA_TFUNCTION		6
#define LUA_TUSERDATA		7
#define LUA_TTHREAD		8
```

