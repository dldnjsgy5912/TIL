보통 사이트 들을 보면 렌딩페이지를 제외하고 대부분에 사이트는 인풋 즉 폼을 컨트롤 하는 것이 대부분일 것 입니다.
React 및 Next 환경에서의 인풋을 컨트롤 하는 경우는 보통 useState 를 사용해서 컨트롤 하는것이 일반적일것입니다.
그리고 많은 사람들이 Mui 를 사용하여 인풋값을 관리하고있죠.

```
  const LoginPage = () => {

  		const [email, setEmail] = useState("");
 	 const [pw, setPw] = useState("");

  return (
  <>
         <div>
            <TextField
              id="adminUsrId"
              placeholder="E-mail"
              fullWidth
              InputLabelProps={{
                shrink: true,
              }}
              inputProps={{ maxLength: 100 }}
              onChange={(e) => setEmail(e.target.value)}
              error={!email || email === ""}
              helperText={
                !email || email === "" || email === undefined
                  ? "Please enter your e-mail."
                  : `${email.length !== 100 ? email.length : 100} / 100`
              }
            />
          </div>

          <div>
            <TextField
              id="adminPass"
              type="password"
              name="password"
              placeholder="Password"
              inputProps={{ maxLength: 30 }}
              fullWidth
              onChange={(e) => setPw(e.target.value)}
              error={!pw || pw === ""}
              helperText={
                !pw || pw === "" || pw === undefined
                  ? "Please enter a password."
                  : `${pw.length !== 30 ? pw.length : 30} / 30`
              }
            />
          </div>
         <button className="green"> Reset Password</button>
  </>
```

위에 코드는 Mui 를 사용한 로그인 로직입니다.
보다싶이 useState 와 onChange 를 이용하여 인풋값을 관리하고 추가로 에러문과 helperText 를 조건문으로 사용하고있습니다.

2개의 인풋을 관리하여야 하기 때문에 useState 도 2 개가 늘어난 것을 볼수있습니다.
그럼 인풋이 10개면 10개를 만들어야 하는 상황이 올수있습니다.
이런 방식은 비효율적이고 코드를 더럽게 만들기 때문에 고민하던중 사용하기 좋은 라이브러리를 발견하였습니다.

```
  import { Controller, useForm } from "react-hook-form";

  const LoginPage = () => {

  	  const { handleSubmit, control } = useForm();
  // ----------- functions ---------------
  const onSubmit = (data: any) => {
    console.log(data);
  };
  return (
  <>
   <form onSubmit={handleSubmit(onSubmit)}>
         <div>
            <Controller
                name="email"
                control={control}
                defaultValue=""
                rules={{ required: "Please enter your e-mail." }}
                render={({
                  field: { onChange, value },
                  fieldState: { error },
                }) => (
                  <TextField
                    id="adminUsrId"
                    placeholder="E-mail"
                    fullWidth
                    InputLabelProps={{
                      shrink: true,
                    }}
                    inputProps={{ maxLength: 100 }}
                    value={value}
                    onChange={onChange}
                    error={!!error}
                    helperText={error ? error.message : `${value.length}/100`}
                  />
                )}
              />
          </div>

          <div>
           <Controller
                name="password"
                control={control}
                defaultValue=""
                rules={{ required: "Please enter your Password." }}
                render={({
                  field: { onChange, value },
                  fieldState: { error },
                }) => (
                  <TextField
                    id="adminPass"
                    type="password"
                    name="password"
                    placeholder="Password"
                    inputProps={{ maxLength: 30 }}
                    fullWidth
                    value={value}
                    onChange={onChange}
                    error={!!error}
                    helperText={error ? error.message : `${value.length}/30`}
                  />
                )}
              />
          </div>
         <button className="green"> Reset Password</button>
        </form>
  </>
```

React Hook Form에서 mui를 사용하려면 Controller 을 사용하여 render 시키면 쉽게 사용 가능합니다.

React Hook Form 를 사용하면 useState 를 사용하여 인풋값은 관리 하지 않아도 되며 onSubmit 으로 들어온 인풋 데이터 값이 객체 형태로 반환되어 쉽게 사용할수 있게 됩니다.
