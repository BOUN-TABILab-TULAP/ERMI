## How to run using Docker
1. Clone the repo
```bash
git clone https://github.com/BOUN-TABILab-TULAP/ERMI.git
```
2. Launch a terminal in the root directory of the repo and build the Docker image where
- `-t` is the tag for the Docker image. You can provide any name you want
- `.` is the relative path to the Dockerfile 
```bash
docker build -t ermi .
```
3. Run the Docker image where
- `-d` indicates "detach", let the container run in the background
- `-p 5000:5000` indicates mapping port 5000 of the container to the port 5000 of the host.
```bash
docker run -d -p 5000:5000 ermi
```
4. Send a POST request
- via curl
    ```bash
    curl -X POST http://localhost:5000/evaluate 
   -H 'Content-Type: application/json' 
   -d '{"textarea":"Sonunda anlaşmaya karar verdik ve önemli bir noktaya dikkat çektik bunun üzerine."}'

   > {'text': 'ID\tFORM\tLEMMA\tUPOS\tXPOS\tFEATS\tHEAD\tDEPREL\tDEPS\tMISC\tPARSEME:MWE \n1\tSonunda\tsonunda\tADV\t_\t_\tkarar\tadvmod\t_\t_\t*\n2\tanlaşmaya\tanlaşma\tVERB\t_\t_\tkarar\tnmod\t_\t_\t*\n3\tkarar\tkarar\tNOUN\t_\t_\tnoktaya\tnmod\t_\t_\t1:LVC.full\n4\tverdik\tver\tVERB\t_\t_\tkarar\tcompound\t_\t_\t1\n5\tve\tve\tCCONJ\t_\t_\tönem\tcc\t_\t_\t*\n6\tönem\tönem\tNOUN\t_\t_\tnoktaya\tnmod\t_\t_\t*\n7\tli\tli\tADP\t_\t_\tönem\tcase\t_\t_\t*\n8\tbir\tbir\tNUM\t_\t_\tnoktaya\tdet\t_\t_\t*\n9\tnoktaya\tnokta\tNOUN\t_\t_\tdikkat\tnmod\t_\t_\t*\n10\tdikkat\tdikkat\tNOUN\t_\t_\tüzerine\tnmod:poss\t_\t_\t2:VID\n11\tçektik\tçek\tVERB\t_\t_\tdikkat\tcompound\t_\t_\t2\n12\tbunun\tbu\tPRON\t_\t_\tdikkat\tcompound\t_\t_\t*\n13\tüzerine\tüzer\tNOUN\t_\t_\tüzerine\troot\t_\t_\t*\n14\t.\t.\tPUNCT\t_\t_\tüzerine\tpunct\t_\t_\t*\n\n'}
    ```
- via Python's requests library
    ```python
    import requests
    res = requests.post('http://localhost:5000/evaluate', json={'textarea':'Sonunda anlaşmaya karar verdik ve önemli bir noktaya dikkat çektik bunun üzerine.'})
    print(res.json())

    > {'text': 'ID\tFORM\tLEMMA\tUPOS\tXPOS\tFEATS\tHEAD\tDEPREL\tDEPS\tMISC\tPARSEME:MWE \n1\tSonunda\tsonunda\tADV\t_\t_\tkarar\tadvmod\t_\t_\t*\n2\tanlaşmaya\tanlaşma\tVERB\t_\t_\tkarar\tnmod\t_\t_\t*\n3\tkarar\tkarar\tNOUN\t_\t_\tnoktaya\tnmod\t_\t_\t1:LVC.full\n4\tverdik\tver\tVERB\t_\t_\tkarar\tcompound\t_\t_\t1\n5\tve\tve\tCCONJ\t_\t_\tönem\tcc\t_\t_\t*\n6\tönem\tönem\tNOUN\t_\t_\tnoktaya\tnmod\t_\t_\t*\n7\tli\tli\tADP\t_\t_\tönem\tcase\t_\t_\t*\n8\tbir\tbir\tNUM\t_\t_\tnoktaya\tdet\t_\t_\t*\n9\tnoktaya\tnokta\tNOUN\t_\t_\tdikkat\tnmod\t_\t_\t*\n10\tdikkat\tdikkat\tNOUN\t_\t_\tüzerine\tnmod:poss\t_\t_\t2:VID\n11\tçektik\tçek\tVERB\t_\t_\tdikkat\tcompound\t_\t_\t2\n12\tbunun\tbu\tPRON\t_\t_\tdikkat\tcompound\t_\t_\t*\n13\tüzerine\tüzer\tNOUN\t_\t_\tüzerine\troot\t_\t_\t*\n14\t.\t.\tPUNCT\t_\t_\tüzerine\tpunct\t_\t_\t*\n\n'}
    ```
