>Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
>
>restricted 권한인가 싶어서요 이거 한번 해주시겠어요? 


>Get-PSDrive -PSProvider FileSystem
>
>이걸로 용량 확인해주시고 ,
>
>$env:PSModulePath -split ';'
>
> PowerShell 모듈 경로확인해서 이거 외로 다른 쪽으로 돌릴수잇는지 확인해보면 좋을 거같아요.
> 특히 이런 경우에, onedrive등의 다른 솔루션이랑 같은 path를 쓰면 발생할수잇어요 
