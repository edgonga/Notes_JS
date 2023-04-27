# -----------------------> Falsified the return of a function

For instance, we want that the method path.join in our test, return always and invented path like: "fake_route/file.txt"
So, we mock that function like this:


```js
jest.mock("path", () => ({
    join: jest.fn(() => 'fake_route/file.txt'
}))
```


Or another way is by using a method of Jest's library:

```js
const mockReaderDir = jest.fn().mockResolvedValue(["file1.txt", "file2.txt"])
```

# -----------------------> Mock and make observable a function

If what we want to do is mocked a function in order to observe it this is what we need:

```js
    const mockReaderDirEquivalent = jest.fn().mockResolvedValue([])
    const mockReaderFile = jest.fn()
    const mockReverser = jest.fn()
    const mockWriter = jest.fn()

    await processFiles(mockReaderDirEquivalent, mockReaderFile, mockWriter, mockReverser)
```

Here, we can see that the first const declared is the same example as the last case, so we ignore it
but for the following three const declared, we mocked and make them observable. However, we didn't link to their orignal function
(mockWriter is the mock function and writer is the original function)
We make this link when we call processFiles and by calling mockWriter as the third parameter is when the link occurs
