1. What is WadB
2. parameters
3. service
	1. WandB
	2. WandB Server
		1. Private Hosting
			1. Personal
				1. Free
			2. Enterprise
				1. Pricing
		2. Cloud Hosting

mysql://root:myrootpw@127.0.0.1:3306/wandb-local-demo


WandB
1. losss
2. image -> epochd
3. training resource monitoring

1. Sweep
2. Wandb Launcher

 docker run --rm -d \
   -e HOST=https://183.110.62.28 \
   -e LICENSE="eyJhbGciOiJSUzI1NiIsImtpZCI6InUzaHgyQjQyQWhEUXM1M0xQY09yNnZhaTdoSlduYnF1bTRZTlZWd1VwSWM9In0.eyJjb25jdXJyZW50QWdlbnRzIjoxLCJ0cmlhbCI6ZmFsc2UsIm1heFN0b3JhZ2VHYiI6MTAsIm1heFRlYW1zIjowLCJtYXhVc2VycyI6MSwibWF4Vmlld09ubHlVc2VycyI6MCwibWF4UmVnaXN0ZXJlZE1vZGVscyI6MiwiZXhwaXJlc0F0IjoiMjAyNC0xMC0xMlQyMzozODo1Ny4zMDlaIiwiZGVwbG95bWVudElkIjoiMzVjZGIyMTMtOTUzYi00ZDFjLWIyMjEtZGZlOGEzOTViYzg3IiwiZmxhZ3MiOltdLCJhY2Nlc3NLZXkiOiI1YWFkMThkNi0zOGQ0LTRmMjktYWZmNi04MTUyMTkwOTUxNjgiLCJzZWF0cyI6MSwidmlld09ubHlTZWF0cyI6MCwidGVhbXMiOjAsInJlZ2lzdGVyZWRNb2RlbHMiOjIsInN0b3JhZ2VHaWdzIjoxMCwiZXhwIjoxNzI4Nzc2MzM3fQ.LopfOQDmTP543nGXktDa-ZNPmn2ddjganofuOf1OUExtZWZ52digGZ64lU_Wr-TX-sjYcpwhmd12YJBTMABECiDI7fH3k1X6CGf020tpQomcuHBKLvwI7RiVf_LtEd-5mREQXVudaKbdN63FSPJO2sHiNDbxgUjYLQ1bw2xlpQvZAy692zFDCDCsX0aVhm5pETl1pEYjOP8Zh0L2uOk3TPUGANYUGH5vCo4hMokF4ciE5FoYaAbupwG7oDUUzZmUNwfq_gvtcFQnu35AzaCVbAjfIe52RUQVvm7QepoIl4CL3nNX19KOAA0gPJhwPW-T3UvI-8jqrKAonL744Z-g-A" \
   -p 28080:28080 -t wandb/local:0.43.0