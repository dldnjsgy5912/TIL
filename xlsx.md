> xlsx 와 file-saver 를 사용하여 엑셀변환

```
yarn add xlsx
```

```
yarn add file-saver
```

```javascript

  //엑셀 설정 변수
  const excelFileType =
    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=UTF-8";
  const excelFileExtension = ".xlsx";
  const excelFileName = "후기 데이터";

  //엑셀 다운로드 이벤트
  const excelDownload = (excelData: any) => {
    const ws = XLSX.utils.aoa_to_sheet([
      [],
      [],
      [day[0], day[1]],
      [
        ...headTitles,
        "데이터제목1",
        "데이터제목2",
        "데이터제목3",
        "데이터제목4",
        "데이터제목5",
        "데이터제목6",
        "데이터제목7",
      ],
    ]);
    excelData.map((data: any) => {
      XLSX.utils.sheet_add_aoa(
        ws,
        [
          [
            data.데이터제목1,
            data.데이터제목2,
            data.데이터제목3,
            data.데이터제목4,
            data.데이터제목5,
            data.데이터제목6,
            data.데이터제목7,

          ],
        ],
        {
          origin: -1,
        }
      );
      ws["!cols"] = [
        //<-- 행 사이즈
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
        { wpx: 100 },
      ];
      return false;
    });
    const wb: any = { Sheets: { data: ws }, SheetNames: ["data"] };
    const excelButter = XLSX.write(wb, { bookType: "xlsx", type: "array" });
    const excelFile = new Blob([excelButter], { type: excelFileType });
    FileSaver.saveAs(excelFile, excelFileName + excelFileExtension);
  };

...

  <Button
            className="red"
            variant="contained"
            onClick={() => {
              excelDownload(listExcel);
            }}
          >
            엑셀 다운로드
          </Button>
```
