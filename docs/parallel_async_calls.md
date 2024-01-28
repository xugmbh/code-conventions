## Calling parallel async operations

Sometimes we can encounter with multi lines of async operations. If they are not dependant on each other, then calling them in Parallel will increase optimization of the code.

E.g:

```ts
  async triggerUserDelete(
    input: Partial<User & { id: string }>
  ): Promise<UserModel> {
    const userDoc = await this.getUserById(input.id);

    this.userCheckCasesService.isExists(userDoc);

    await this.removeUserFromWhiteList(userDoc);

    await this.revokeUserInvitation(userDoc);

    await this.removeUserFromClerk(userDoc);

    await userDoc.deleteOne();

    return userDto(userDoc);
  }
```




We can refactor for sure. However, the question is more about how we handle the errors or is the operations are okay to fail individually? That concern is more about feature design principle and how it should fail gracefully. Currently it is up to the engineering team to decide as we are missing proper feature architect.


```ts
  async triggerUserDelete(
    input: Partial<User & { id: string }>
  ): Promise<UserModel> {
    const userDoc = await this.getUserById(input.id);

    const [removeUserFromWhiteListResult, revokeUserInvitationResult, removeUserFromClerkResult, userDocDeleteResult] = await Promise.allSettled([
      this.removeUserFromWhiteList(userDoc),
      this.revokeUserInvitation(userDoc),
      this.removeUserFromClerk(userDoc),
      userDoc.deleteOne()
    ]);

    this.userCheckCasesService.hasError(removeUserFromWhiteListResult);
    this.userCheckCasesService.hasError(revokeUserInvitationResult);
    this.userCheckCasesService.hasError(removeUserFromClerkResult);
    this.userCheckCasesService.hasError(userDocDeleteResult);

    return userDto(userDoc);
  }
```