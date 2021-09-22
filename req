"""Python program to execute
Sent different type of HTTP Request"""
import requests


class Req:
    def __init__(self):
        self._reqUrl = None
        self._reqHeader = None
        self._reqMethod = None
        self._reqResponse = None

    @property
    def reqUrl(self):
        return self._reqUrl

    @reqUrl.setter
    def reqUrl(self, inUrl):
        self._reqUrl = inUrl

    @property
    def reqData(self):
        return self._reqData

    @reqData.setter
    def reqData(self, inData):
        inDict = dict((x.strip(), y.strip())
                      for x, y in (element.split(':')
                                   for element in inData.split(', ')))
        self._reqData = inDict

    @property
    def reqHeader(self):
        return self._reqHeader

    @reqHeader.setter
    def reqHeader(self, inHeader):
        if inHeader == '':
            self._reqHeader = None
        else:
            dicHeader = dict((x.strip(), y.strip())
                             for x, y in (element.split(':')
                                          for element in inHeader.split(', ')))
            self._reqHeader = dicHeader

    @property
    def reqMethod(self):
        return self._reqMethod

    @reqMethod.setter
    def reqMethod(self, inMethod):
        self._reqMethod = inMethod

    @property
    def reqResponse(self):
        return self.reqResponse

    @reqResponse.setter
    def reqResponse(self, inResponse):
        self._reqResponse = inResponse

    def send_req(self):
        req = requests.session()
        if self._reqMethod == 'post':
            self._reqRespons = req.post(url=self._reqUrl, data=self._reqData, headers=self._reqHeader)
        if self._reqMethod == 'json':
            self._reqRespons = req.post(url=self._reqUrl, json=self._reqData, headers=self._reqHeader)
        elif self._reqMethod == 'get':
            self._reqRespons = req.get(url=self._reqUrl)
        else:
            print('Request Type Error')

    def receive_req(self):
        print('HTTP-REQUEST:\n')
        print('**********************************')
        print(self._reqRespons.request.url)
        print(self._reqRespons.request.method)
        print(self._reqRespons.request.headers)
        print(self._reqRespons.request.body)
        print('**********************************')
        print('HTTP-RESPONSE:\n')
        if self._reqRespons.status_code == 200:
            print('HTTP-Status = Success')
            for i in self._reqRespons.headers:
                print(i, ': ', self._reqRespons.headers[i])
            if self._reqMethod == 'json':
                print(self._reqRespons.json())
            else:
                print(self._reqRespons.content)
        elif self._reqRespons.status_code == 302:
            print('Redirect')
        elif self._reqRespons.status_code == 401:
            print('Unauthorized')
        elif self._reqRespons.status_code == 403:
            print('Forbiden')
        elif self._reqRespons.status_code == 404:
            print('Not Found')
        elif self._reqRespons.status_code == 500:
            print('Internal Server Error')
        elif self._reqRespons.status_code == 502:
            print('Bad Gateway')
        elif self._reqRespons.status_code == 503:
            print('Service Unavailable')
        elif self._reqRespons.status_code == 504:
            print('Gateway Timeout')
        else:
            print('Response Code:', self._reqRespons.status_code)


if __name__ == "__main__":
    httpReq = Req()
    httpReq.reqUrl = input('Enter URL\t Ex:https://domain.com\n').lower()
    httpReq.reqMethod = input('Enter HTTP Method\t EX: POST, GET or JSON\n').lower()
    if httpReq.reqMethod == 'post':
        httpReq.reqData = input('Enetr DATA\t Ex: name:book, number:2\n')
    if httpReq.reqMethod == 'json':
        httpReq.reqData = input('Enetr JSON\t Ex: name:book, number:2\n')
    httpReq.reqHeader = input('Enter HEADER\t User-Agent: Mozila, **if there is no header just enter**\n')
    httpReq.send_req()
    httpReq.receive_req()
